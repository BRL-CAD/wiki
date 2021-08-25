# Development Logs

## Project Details

|                     |                                                         |
|---------------------|---------------------------------------------------------|
| **Project Name**    | STEP Libraries: Improving Thread Safety and Performance |
| **Project Student** | Pulkit Mittal                                           |
| **IRC(nick)**       | hoiji                                                   |
| **Github (handle)** | hoiji09                                                 |

## Milestones

### Compulsary

-   Thread Safety in cllazyfile *Status*: Review Awaiting
-   Thread Safety in clstepcore *Status*: Review Awaiting
-   Thread Safety in cleditor *Status*: Review Awaiting
-   Thread Safety in cldai *Status*: Review Awaiting

### Bonus

In this section I will list down all other modifications which I did
during the GSOC period.

-   Single threaded performance optimizations
    -   Removed *istream \*in2* from *STEPfile::AppendFile*. Originally
        for the second pass a new *istream (in2)* was being created and
        the *.step* file was being opened again. This was prevented by
        directing the original *istream (in)* to the beggining of the
        *.step* file.
-   Code Refractoring
    -   In libraries clstepcore and cldai, there were few classes which
        were very similar. The logic common to these classes was
        indentified and removed, a new class was created which had that
        common logic. The original classes were made to inherit from the
        new class. This removed duplicated code and also made making
        changes (for thread safety) easier.

## GSOC Period

### Week 1

**17 May (Sat):**

-   Figured out various functionalities in cllazyfile step library which
    should be made thread safe.
    These are
    1.  Opening multiple files in parallel.
    2.  (lazy) loading separate SDAI_Application_instance in parallel.
    3.  Reading the forward / backward references of instances in
        parallel.
    4.  Finding instances belonging to same / different types in
        parallel.
    5.  Initializing / Setting the registry in parallel.
    6.  Registering Data Sections in parallel

<!-- -->

-   Strategizing how the various features will be added into the code.
    Firstly a test will be created to note the existance of thread
    safety for the above features. If the test fail then appropriate
    coding will be done

**18 May (Sun):**

-   A test was created in *lazy_thread_safety_test.cc* file, to check
    the concurrent read safety of *getFwdRefs()* and *getRevRefs()* and
    expectedly it failed.
-   *Note:* to run the test, the CMakeFiles:
    *cmake/SC_CXX_schema_macros.cmake* &
    *src/cllazyfile/CMakeLists.txt* were slightly messed up.

**19 May (Mon):**

-   Introduced *getFwdRefsSafely* and *getRevRefsSafely* which are
    thread safe. The thread safety test in
    *lazy_thread_safety_test.cc* passed. Submitted code through git
    in a branch called hj/cllazyfile-thread-safety.
-   Discussed with mentor about the importance order of functionalities
    mentioned above. Hence will be covering the functionalities in the
    following order 3(done)&gt;4&gt;2&gt;1&gt;6

**20-21 May (Tue, Wed):**

-   Noticed that *getFwdRefsSafely* and *getRevRefsSafely* are consume
    memory each time they are called (as separate clones are made for
    each invocation). (Blame the use of Judy Structure) The memory is
    freed only when destructor of *lazyInstMgr* is called. One way
    around this problem was to let the user call a function (say)
    *returnFwdRefsSafely* which would release the space related to a
    clone. Hence, I spent 2 days trying to modify the original judy code
    so that it allows closure of clones. But as I was not able to get a
    breakthrough, I have left this task for later.

**22 May (Thu):**

-   Created a test to check the thread safety of *getInstances* (*i.e.*
    finding instances belonging a specific type). As expected the test
    failed when the number of invocations were very high. This is
    because *getInstances* internally uses *find* operation which is not
    thread safe.

**23 May (Fri):**

-   Added the thread-safe *getInstancesSafely* and
    *countInstancesSafely*. Also submitted the code in github.

### Week 2

**24 May (Sat):**

-   Started working towards making lazy-loading of instances thread
    safe.
    -   Created a test which would spawn two threads which try to load
        instances.
        -   In the first half of iterations the threads would try to
            load same set of instances.
        -   In the second half of iterations the threads would try to
            load different set of instances (not necessary disjoint).
        -   For each thread within one iteration an instance would be
            loaded twice. This checks the case where the instance may or
            may-not be already loaded and the case where the instance is
            already loaded.
    -   The problem that arose during the compilation of the test was
        that, finally the *_mainRegistry* was being used, and I had
        very little idea about the schemas and registries. It could not
        find the *schema.h* file.
-   Couldn't work the earlier half of the day as I was traveling.

**25 May (Sun):**

-   Got the thread safety test for lazy-loading to compile by doing
    certain changes in the *src/cllazyfile/CMakeLists.txt*.
    -   This was done by including the directory
        *${CMAKE_BINARY_DIR}/schemas/sdai_cd209* for the above test.
    -   The restriction that the above changes imposed on
        *lazy_thread_safety_test* was that, now it has to be given
        the the step file *data/cd209/ATS1-out.stp* as input.
-   A potential bug was found while running the above test. The bug
    would appear if we follow the following steps
    1.  *lazyInstMgr \* mgr = new lazyInstMgr;*
    2.  *mgr-&gt;initRegistry( SchemaInit );*
    3.  *mgr-&gt;openFile( fileName );*
    4.  *delete mgr*
    5.  *lazyInstMgr \* mgr = new lazyInstMgr;*
    6.  *mgr-&gt;initRegistry( SchemaInit );*

    -   The last step would cause assertion failure in function
        *setRegistery*. (i.e. *assert( _mainRegistry == 0 )*). This was
        solved by explicitly initializing *_mainRegistry* with '0'
        inside the *lazyInstMgr* constructor.
-   When the test was run on the original *loadInstance* function, it
    gave assertion error related to the input stream.
-   Saw the comments posted by Mark on my earlier commits. I decided to
    make corresponding changes in the code, once I had made lazy-loading
    thread safe

**26 May (Mon):**

-   A thread-safe version of *loadInstance* was created. For this a fat
    lock was used. It is possible that we can make the lock application
    finer, however that has been left for later. This version passed the
    test successfully.
    -   However their appeared to be some problem in the step file,
        because loading of one particular instance always failed,
        irrespective of the number of threads. A temporary fix was
        applied by removing a newline character from the step file.
    -   In the *loadInstance* function, their was an issue of a warning
        *instance \#... not found in any section* appearing even if the
        instance was found in the *_instancesLoaded* list. The fix was
        trivial
-   A thread safe counterpart to *mgr-&gt;getAdapter()-&gt;FindFileId(
    instanceID )-&gt;GetSTEPentity()* was made. This was slightly
    complicated then the previous features as it consisted of 2 complex
    steps in different classes. Both being thread unsafe.
    -   For this each thread was assigned its own mgrNodeHelper. This
        mgrNodeHelper was created once, for each thread and reused on
        later invocations.
    -   Dependency was taken on thread safe *loadInstanceSafely*
    -   The counterpart was also successfully tested

**27 May (Tue):**

-   As per the advice given by Mark, the macro *HAVE_STD_THREAD* was
    utilized in *CMakeLists.txt*, including header files, mutex / thread
    safe functions declarations etc.
    -   This opportunity was also used to clean up the *CMakeLists.txt*
-   Fixed the newline issue encountered on 26th May. This was done by
    modifying the lazyfile parser by instructing it to ignore the
    newlines in such cases. The temporary fix was reverted back as it
    was no longer required.
-   Prepared the changes done from 24th May in the form of multiple
    commits. Also the thread safe code was clubbed together wherever
    possible for easy identification.

**28 May (Wed):**

-   While introducing *HAVE_STD_THREAD* in
    *src/cllazyfile/lazyTypes.h* a compilation problem was encountered.
    Somehow *HAVE_STD_THREAD* macro was not being recognized by
    *lazyTypes.h*. This was surprising as *HAVE_STD_THREAD* was
    recognized by *lazyInstMgr.cc*. The final solution was to explicitly
    declare *HAVE_STD_THREAD* through the compiler flag in
    *src/cllazyfile/CMakeLists.txt*.
-   Also continuing from the last point in 27th May, the work done from
    24th May was organized into 12 different commits and submitted to
    github.

**29 May (Thu):**

-   Started adding a test for checking thread safety in while opening
    multiple files in parallel, using the same lazyInstMgr.
    -   The first and foremost problem was identifying the data
        structures of the lazyInstMgr whose state would change when
        *lazyInstMgr::openFile()* is called. Unlike the previous
        functionalities here more then one data structures were
        involved. The following data structures were identified.
        -   *instanceRefs_t _fwdInstanceRefs*
        -   *instanceRefs_t _revInstanceRefs*
        -   *instanceTypes_t \* _instanceTypes*
        -   *instanceStreamPos_t _instanceStreamPos*
        -   *dataSectionReaderVec_t _dataSections*
        -   *lazyFileReaderVec_t _files*
        -   *unsigned long _lazyInstanceCount*
        -   *int _longestTypeNameLen*
        -   *std::string _longestTypeName*
    -   The test would create two instances of lazyInstMgr, through
        first it would call openFile for two different files in a serial
        manner, through second it would call openFile for these two
        files parallely. Later it would compare the above data
        structures of both the instance managers and report any
        discrepancy it finds.

**30 May (Fri):**

-   The above test was completed.
    -   An extra lazyInstMgr API was added to get *_instanceStreamPos*
        data structure for comparison.
    -   The test when run on existing openFile failed. Multiple reasons
        were attributed to the failure by running the test multiple
        times. Apart from gracefully failing, the test also failed many
        times due to *segmentation fault* or an assertion failure in the
        *cllazyfile parser*.

<!-- -->

-   Work was started on making the openFile thread safe.

### Week 3

**31 May (Sat):**

-   At this I was going through the dilemma of following the convention
    of creating different functions for thread safe code vs. using
    macros for demarcating code used for ensuring thread safety.
    -   Continuing the former meant code duplication.
    -   Switching to the latter meant that flexibility of letting the
        user decide which function he wants to call is thrown away.
    -   I finally took the middle way decision which didn't had any of
        the above problem.
        -   All calls to the *mutex* are now through a wrapper which
            directs the call to the *mutex* functionality if
            *HAVE_STD_THREAD* is defined or else to a dummy function
            which does nothing.
-   In the thread safe counterpart of *openFile*, *openFileSafely* fine
    grain locking was done.
    -   Mutexes were added at to safe-gaurd their respective data
        structures
    -   Functionalities such as *lazyInstMgr::registerDataSection* were
        converted into a two step process.
    -   Since it was now possible that an element of the *_dataSection*
        vector can be null the destructor for *lazyInstMgr* was changed
        accordingly.

**1 June (Sun):**

-   The test for checking thread safety was still failing, due to
    assertion failure in the *cllazyfile parser*.
    -   It was found that this is due to a *static* variable in
        *sectionReader::getDelimitedKeyword*. The function was reworked
        and named *fillDelimitedKeyword*. The functions taking
        dependence on this were slightly modified to reflect this
        change.
    -   Another static variable in *p21HeaderSectionReader* was
        identified and tackled with.
-   The test finally succeeded. Some performance statistics
    -   File A: *3tnv70-asa.stp* (\~45mb) was taken from the site
        examples.
    -   File B: *gtc01-mme01_asm.stp* (\~45mb) was taken from
        *<http://downloads.openmoko.org/developer/CAD/Neo1973_IGES_STEP.zip>*
    -   It took \~9 seconds if we tried to open either File A or File B.
    -   It took \~17 seconds if we tried to open File A and then File B.
    -   It took \~12.5 seconds when both the files were opened in
        parallel.

**2 June (Mon):**

-   The locking in *loadInstanceSafely( instanceID )* was made finer.
    -   Double checking was also done to enhance performance in cases in
        which say:
        1.  Thread A is creating a *realObject* belonging to instance
            *x*.
        2.  Thread B comes and wants to get an object belonging to
            instance *y*.

        -   If instance *y* has been already loaded then Thread B
            doesn't have to wait for Thread A. This is now handled.
-   The work done from 29th May was organized into different commits and
    pushed to github.

**3 June (Tue)**

-   Going through the code in *src/clstepcode*
    -   Learnt about the various files in the library.
    -   Several Problems were identified:
        -   The amount of code is huge.
        -   What makes the problem worse is that there are lots of small
            classes. Since a TDD approach is being followed it means
            that there will have to be lots of test files.

**4-6 June (Thu - Fri)**

-   Very Little work done due to family reunion + travelling.

### Week 4

**7 June (Sat)**

-   Unsuccesfully tried to figure out a way to run the tests such as
    *src/clstepcore/test/test_operators_STEPattribute.cc* on my remote
    machine.
-   Created a mutex wrapper: *sc_mutex* that will contain *std::mutex*
    and call its lock, unlock function if *HAVE_STD_THREAD* is
    enabled. If on the other hand *HAVE_STD_THREAD* is disabled, the
    wrapper will not contain *std:mutefx* and will call the dummy lock,
    unlock functions.
    -   I will modify cllazyfile to take dependency on it later.

**8 June (Sun)**

-   Changed the branch name from *hj/cllazyfile-thread-safety* to
    *hj/thread-safety*. Now I will keep all the thread-safe code in one
    branch.
-   Modified the *CMakeLists.txt* of each of the library.
    -   It was also found that some of the tests used the header files
        directly. Hence the cmake files of such libraries will have to
        be changed when required.

**9 June (Mon)**

-   The test for checking thread safety of *instmgr* was started.
    -   The functions whose thread safety would be checked was append
        and delete functions.
    -   Three test scenrios were checked:
        1.  Two threads appending *SDAI_Application_instance* pointers
            to the same *instmgr*.
        2.  Two threads deleting *SDAI_Application_instance* pointers
            to the same *instmgr*.
        3.  One thread appeding *SDAI_Application_instance*pointers
            and other thread trying to delete some other pointers from
            the same *instmgr*.

**10 June (Tue)**

-   The test for checking thread safety of *instmgr* was completed. It
    was named as *InstMgr_thread_safety_test* and put into
    *src/clstepcore* directory.
    1.  In each of the test cases before the insertion / deletion
        happens on one InstMgr sequentially and other parallely.
    2.  These two are later compared for any disparity.
-   On each run either *InstMgr_thread_safety_test* failed gracefully
    (i.e a disparity was found between two InstMgr) or a seg. fault was
    encountered.

**11 June (Wed)**

-   Their was some duplicate code in *instmgr* class for *GetSTEPentity*
    function. Even though the function is obselete, the duplicated code
    was removed.
-   Code was written to make *InstMgr* Append and Delete function thread
    safe.
    -   This involved some amount of code refractoring and introduction
        of a mutex.
    -   A compilation error on invoking *make* prevented any further
        progress.

**12 June (Thu)**

-   Was able to finally compile yesterdays code by changing the file
    *SC_CXX_schema_macros.cmake* in the cmake directory.
-   The *InstMgr_thread_safety_test* passed in all three cases. Some
    incorrect code was also corrected.

**13 June (Fri)**

-   I decided that I will work in the *GenNode* related classes
    (*GenNodeArray*, *GenNodeList*) defined in clutils and the classes
    which inherit from them:
    -   *MgrNode*: *MgrNodeArray*, *MgrNodeArraySorted*, *MgrNodeList*
    -   *DispNode*: *DispNodeList*
-   Some of the code was very badly written (seeing from a thread safety
    perspective)
    -   Ex. The Remove function in *GenNode* modified the state of other
        *GenNode* objects. Typically this should be done by the
        *GenNodeList* class.

### Week 5

**14 June (Sat)**

-   Added *containingList* pointer in *GenericNode*. This pointer will
    point to the list of which the node is part of.
    -   This pointer will used whenever the *GenericNode* or its
        descendent want to perform any operation on the other Nodes.
    -   Such operations will now be directed to the list function whose
        responsibility would be to ensure proper locking.
    -   Added assertions and checks regarding the same.
    -   Also used *containingList* to remove duplicate code.
-   Some of the code was moved between files, to make the code neater.

**15 June (Sun)**

-   Organized the work done until 12 June into commits and pushed it
    into the github repository.
    -   This was done so that *Mark* could review one of the changes
-   Added sc_recursive_mutex.
    -   This will be used to handle situtations where there are 2 public
        APIs (say A, B).
        -   Both modify an internal data structure, hence lock it.
        -   However one API depends on other. (say B depends on A)
    -   Earlier In such cases I used to make a helper function (H) which
        would do the main job. A and B would depend on H and can be
        individually locked.
    -   Having a recursive lock would eleminate the need to do the
        above.
        -   Made *instmgr* lock recursive.

**16 June (Mon)**

-   Corrected locking in *getApplication_Instance*. Earlier (due to my
    carrelessness) their was a possibilty that a thread might never
    release the lock.
-   Modified the insert function in gen/mgr/disp lists.
    -   The new insert function checks whether the existing node belongs
        to the same list or not. If it doesn't it does nothing and
        returns false.
    -   This will be very helpful when introducing thread safety in list
        structures. Ex. take the scenerio:
        -   Thread A wants to insert x after y.
        -   Meanwhile Thread B removes y from current list.
        -   In such a case the thread A's insertion fails.
-   Finally introduced *recursive_mutex* in *gennodelist*.
    *mgrnodelist* which inherits *gennodelist* was also changed
    accordingly.

**17 June (Tue)**

-   Added *GetGenNode* function in *GenNodeArray*.
    -   This function is a safer couterpart to \[\] function.
    -   Replaced call to the \[\] function with calls to *GetGenNode*
        function.
    -   Was feasable since the former is only used for getting
        *GenericNode* pointers.
-   Minor refractoring in *MgrNodeArray* This will be helpful when we
    introduce a mutex in *GenNodeArray*.

**18 June (Wed)**

-   Added *std_recursive_mutex* in *GenNodeArray*. Also modified
    classes which inherit the above accordingly
-   Organized the work done from 14 June into commits and pushed it into
    the github repository.

**19 June (Thu)**

-   Could not work, as I devoted my the whole day to my M.Tech Project.

**20 June (Fri)**

-   Next I decided to work on *ExpDict.h/.cc/.inline.cc* files. These
    define classes representing descriptors for EXPRESS schemas,
    entities, attributes, and types.
    -   These file have around \~50 classes. On going through each of
        them it was found that the potentially thread unsafe classes can
        be divided into categories.
        1.  Classes which define a set data structure for a subclass of
            *Dictionary_instance*
        2.  Classes which inherit from *SingleLinkList* class.
        3.  Some subclasses of *Dictionary_instance* which take
            dependency on std::vector structures or multiple structres
            which should be consistent with each other.

### Week 6

**21 June (Sat)**

-   Added class *Dictionary_instance__set*. This class is intended to
    be a superclass of all the \*__set classes.
    -   These classes are:
        -   *Explicit_item_id__set*
        -   *Implicit_item_id__set*
        -   *Interface_spec__set*
        -   *Global_rule__set*
        -   *Uniqueness_rule__set*
    -   Lot of duplicated code was removed this way.
    -   Making *Dictionary_instance__set* thread safe would now
        ensure thread safety of the above subclasses.

**22 June (Sun)**

-   Made *Where_rule__list* a subclass of
    *Dictionary_instance__set*, as it was found to have similar
    features.
-   Work done from 19 June was organized into commits and pushed to
    github.

**23 June (Mon)**

-   Some missing code in yesterday commits was added and submitted to
    github.
-   Made *Dictionary_instance__set* thread safe by adding a mutex.
-   Made *SingleLinkList* class thread safe by adding a mutex.
    -   Also a cmake file was modified inorder to compile the above
        changes.
-   Made Schema thread safe by using 3 mutexes to protect the
    *_function_list*, *_procedure_list* & *_global_rules* data
    structures.
    -   The first two are vectors.
    -   The last is already a thread safe structure, however its being
        lazy-initilized hence a mutex is needed.
-   Made *Global_rule* thread safe by using a mutex.
    -   Thread safety in functions *entities_* and *where_rules_* was
        being violated

**24 June (Tue)**

-   The next focus was the *Registry* class. A test to check the thread
    safety of Registry class was created.
    -   In it the Entity, Schema and Type operations are tested.
    -   For each, there are 3 checks: Add-Add, Remove-Remove,
        Add-Remove. \*\* For every check the two operation are done
        first serially and then parallely. Their results are then
        compared.
-   The test when run either gracefully failed or gave a segFault in
    every check.

**25 June (Wed)**

-   *The curious case of hashtables*: The *Registry* class took
    dependency on a hashtable data structure defined in
    clutils/sc_hash.h.
    -   These hashtable methods appeared to pass the thread safety
        check, when the number of elements which were to be inserted in
        the hash table were small.
    -   However when lots of element were added into a hash table, an
        internal function of the hashtable *SC_HASHexpand_table* is
        called which is thread unsafe.
    -   Hence it was decided to put a fat-lock around the hash-table.
-   Made Registry *Entity*, *Schema* and *Type* operations thread safe
    by adding a mutex for each.
    -   All the checks in *Registry_thread_safety_test* now pass.
-   The code written from 23 June was organized into commits and pushed
    to github.

**26 June (Thu)**

-   Wrote a blog on my mid-term progress:
    <http://brlcad.org/wiki/User:Pulkit_Mittal/GSOC2014/Midterm>
-   Devoted the rest of the day on M.Tech. Project.

**27 June (Fri)**

-   Devoted the day to M.Tech Project.

### Week 7

**28 June (Sat)**

-   Divided the rest of *stepcore* library into three parts.
    1.  Those who define *STEP* interface. (i.e the STEP\*.h/.cc files)
    2.  Those who define *sdai* interface. (i.e the STEP\*.h/.cc files)
    3.  Classes listed in complexSupport.h and their implementation in
        the associated \*.cc files

    -   It was decided that functions declared in *read_func.h/.cc* and
        *print.cc* files wont be made thread safe as they were not a
        part of the class and thus didn't had any data structures to
        protect.
-   Duplicate code was removed in *STEPaggregrate*. *STEPaggregrate* and
    its superclass *SingleLinkList*.cc had the same destructor.

**29 June (Sun)**

-   Made the classes defined in *STEPaggregrate.h* thread safe.
    -   The function which was identified as a potential thread unsafe
        function was the *ShallowCopy*. This function was common to all
        the subclasses of *STEPaggregrate*.
    -   Thread safety was ensured by relying on the mtx defined in
        *SingleLinkList*. For this reason the mutex was redefined in the
        public scope, as inside the *ShallowCopy* nodes belonging to
        another instance were iterated upon.
-   Efforts were also made to condense all the *ShallowCopy* functions
    into one, so as to decrease the code amount. This attempt however
    failed since the function differed slighly in each of the
    subclasses.

**30 June (Mon)**

-   I had to prepare a presentation for my M.Tech project meeting with
    company funding my project.

**1 July (Tue)**

-   Instead of moving to *STEPattribute*, I decided to focus my
    attention to the classes declared in *complexSupport.h*.
    -   Started with Entnode. It was quite tricky since unlike other
        node-list data structure implementation in the STEP libraries,
        Entnode didn't had any *covering list* (i.e a class with
        variable such as head, tail etc through which the list
        data-structure could be accessed)

**2 July (Wed)**

-   Made *EntNode* of *complexSupport.h* thread safe.
    -   For this I used a recursive mutex in a shared manner. The
        pointer to this mutex was kept with every node.
    -   This shared mutex was initialized when a specialized *EntNode*
        constructor (responsible for creating multiple *EntNodes*) was
        called
    -   The shared mutex would be deleted when the destructor of an
        *EntNode* having a live mutex pointer was called.

**3 July (Thu)**

-   M.Tech project presentation with the company.

**4 July (Fri)**

-   Made SubSuperIterators.h thread safe.
    -   This was done by introducing a recursive mutex meant to protect
        the std::deque 'q' and unsigned integer 'position'
-   Also Removed duplicated code in SubSuperIterators.cc

### Week 8

**5 July (Sat)**

-   Next I focussed towards making *EntList* thread safe. Apparently
    this was very difficult.
    -   Tactics which involved *coarse grain locking* could not be used
        due to the presence of *appendList* function in subclass
        *MultList*.
    -   Tactics which involved *fine grain locking* could not be used as
        some of the functions like *firstNot* iterated over the *next*
        pointer and *lastNot* iterated over the *prev* pointer.

**6-8 July (Sun-Tue)**

-   Thought about the EntList problem. Discussed with my mentor. Posted
    my problem in the *scl-dev* group.
-   Horror strikes!! While talking to my mentor I realized that I had
    forgotten to run the 230 unit tests while making my commits.
    -   Now, when I ran them, about half of them were failing!!
    -   The log file was traced to get clues about why so many test
        failed.
    -   Various commits were checked out to find what was the *bad*
        commit. It was found out that some of the tests which failed
        were due to the recent uncommited work. These mistakes were
        quickly rectified.

**9 July (Wed)**

-   Changes in cmake to build lazy tests. Some changes in cmakefiles had
    caused the test associated with *lazy_test* to stop building. Those
    changes were reviewed and corrected.
-   Corrected *SingleLinkedList* mtx bug. The mtx is converted into
    *sc_recursive_mtx* deleted in the destructor

**10 July (Thu)**

-   Organized *most* of the work done from 26th July into commits and
    pushed them to github.
-   Some of the later tests (about 4) were still failing due todue to
    assertions failures inside a mutex lock. No success as of today.

**11 July (Fri)**

-   Had to devote most of the whole day to checking major scripts (a
    part of my teaching assistant duties. Thankfully now I am free from
    that)

### Week 9

**12 July (Sat)**

-   Modified *add_schema_dependent_test* module.
    -   The assertion failures before was due to the test file not being
        equipped with the *HAVE_STD_THREAD* macro.
    -   The CMakeFile associated with *add_schema_dependent_test* was
        changed and all the tests except of 'test_inverse_attr3' are
        passing.

**13 July (Sun)**

-   Made *STEPattributeList* thread safe.
    -   The functions *STEPattributeList::\[\]* &
        *STEPattributeList::push* were identified as vulnerable.
    -   Instead of declaring a new mutex to protect the state, the mutex
        defined in its superclass *SingleLinkList* was used.
-   Redefined *GetMiEntity* API belonging to
    *SDAI_Application_instance* class.
    -   The function now accepts *const char \** (instead of *char \**)
        as parameter.

**14 July (Mon)**

-   Removed the infinite recursion bug in *STEPattribute*.
    -   This bug was identified few days ago when I was going through
        the code. Finally I was able to discuss it with the mentor.
    -   The bug would surface if a *STEPattribute* instance which has
        been redefined, has its *ShallowCopy* function invoked.

**15 July (Tue)**

-   Added test for checking thread safety of
    *SDAI_Application_instance* class.
    -   This test would check thread safety for *AppendMultInstance* &
        *GetMiEntity* functions in class *SDAI_Application_instance*
        by using two threads two invoke *AppendMultInstance* on the same
        *SDAI_Application_instance* object. A third thread would call
        *GetMiEntity* simultaneously.
    -   Rest of the functions were not checked since the locking in them
        was trivial.
    -   The test failed on the original code.

**16 July (Wed)**

-   Made *SDAI_Application_instance* thread safe.
    -   This was done by introducing a mutex for each
        *SDAI_Application_instance*.
    -   *AppendMultInstance* was made thread safe by doing
        hand-over-hand locking.
    -   GetMiEntity was made thread safe acquiring locks in increasing
        order and releasing locks in decreasing order.
    -   The checks in sdaiApplication_instance_thread_safety_test
        now pass.

**17 July (Thu)**

-   Travelling home.

**18 July (Fri)**

-   Work done from 13 July was divided into different commits and pushed
    into github.

### Week 10

**19 July (Sat)**

-   Locking was done in *ExpDict.cc*.
    -   There were some functions in *ExpDict.cc* that were not properly
        locked before.

**20 July (Sun)**

-   Made *sdaiSelect::CanBe( BASE_TYPE )* thread safe.
-   Started strategizing how to make *STEPcomplex* thread safe.

**21 July (Mon)**

-   Travelling back to university.

**22 July (Tue)**

-   Work done from 19 July was organized into different commits and
    pushed into github.
-   Fixed locking in *sdaiApplication_instance.cc*. The
    *STEPattributeList* data was being iterated and modiefied by the
    *SDAI_Application_instance* class without invoking the mutex of
    the *STEPattribute* class. This was fixed in this commit.
-   Minor *STEPcomplex* optimization.
    -   Collapsed some if conditions into a while condition without
        changing the semantics

**23 July (Wed)**

-   Made *STEPcomplex* thread safe.
    -   The assumption used was that *STEPcomplex* class wont in future
        provide an API through which threads can remove / insert a
        *STEPcomplex* node.
    -   Three already declared mutexes were used in for this purpose:
        1.  A recursive mutex for each *STEPcomplex* node (borrowed from
            the superclass *SDAI_Application_instance*)
        2.  A recursive mutex belonging to *AttrDescriptorList* class
            (originally defined in *SingleLinkList* class)
        3.  A recursive shared mutex belonging to *EntNode* class.

        -   The fixed order between the locks was: (2) &gt; (1). (3) was
            independent.

**24 July (Thu)**

-   Work done from 22 July was organized into different commits and
    pushed into github.
-   Thread safety in *EntList*.
    -   Under the assumptions that an *EntList* object cannot be
        inserted in between two *EntList* objects and cannot be removed
        from a list of *EntList* objects, making this class thread safe
        became trivially easy.
    -   One mutex per *EntList* object was introduced to support
        appending of *EntList* objects. This feature would be used by
        its subclass (*MultList*)

**25 July (Fri)**

-   Thread Safety in *SimpleList*
    -   Used *sharedMtxP* defined in *EntNode* class to protect
        *EntNode* list structure which was being accessed in functions
        of *SimpleList* class
-   Thread safety in *MultList*
    -   The mutex defined in the superclass *EntList* was used in the
        function appendList.

### Week 11

**26 July (Sat)**

-   Thread safety in *JoinList*, *AndList* & *AndOrList*
    -   *sharedMtxP* of *EntNode* class was invoked to keep the list of
        *EntNode* consistent whenever the *EntNode* list was being used
        multiple times in a function belonging to any of the above
        classes.

**27 July (Sun)**

-   Thread safety in *OrList*
    -   Strategy adopted was similar to *AndList*. However the mutex
        belonging to the superclass *EntList* was used to protect
        various counters (choiceCount, choice) used by *OrList*

**28 July (Mon)**

-   Thread safety in *ComplexList*
    -   Like the classes before, used *sharedMtxP* to protect the
        *EntNode* list whenver it was being iterated upon.
    -   Also added a public mutex to protect the public next pointer.
        Resposibilty of using it will fall to the class which is using
        next pointer (*ComplexCollect*)

**29-31 July, 1 August (Tue-Fri)**

-   Was down with fever (the first couple of days), followed by eyes
    pain and weakness. Was advised to take a bed rest.

### Week 12

**2 August (Sat)**

-   Thread Safety in *ComplexCollect*
    -   A mutex was introduced to proctect the counter and the pointer
        to *clists*.
    -   The insert and remove functions were tricky to make thread safe
        as *clists* may or may-not have been initialized. Hand-over-hand
        locking was used.
    -   Note: In the function *ComplexCollect::supports( EntNode )*,
        there was a piece of code present in which the next and prev
        pointer of an EntList were being modified.
        -   This could have ruined the thread safe strategy for making
            *EntList* thread safe. (violated our assumption)
        -   The reason it didn't was that, that *EntList* was created
            locally.

**3 August (Sun)**

-   Work done from 24 July was organized into commits and pushed to
    github.
-   Made *ReplicateList* in *cleditor* thread safe.
    -   Used *mtxP* of the superclass *SingleLinkList* to ensure thread
        safety
-   Thread safety in *CmdMgr* of *cleditor*

**4 August (Mon)**

-   Not much work done as it was a heavy day in college

**5 August (Tue)**

-   Made *DirObj* of *clutils* thread safe.
    -   This was achieved introducing a mutex in the *DirObj* class.
    -   Course-Level (fat) Locking was done only in publically accessed
        function.

**6 August (Wed)**

-   Work done from 3 August was organized into commits and pushed to
    github.

**7 August (Thu)**

-   Converted *GetKeyword* to *FillKeyword*.
    -   In the original function a *static string* was being used.
    -   The dependency on the static string was removed by passing a
        string as a parameter from the caller to callee, so that the
        function could operate without worrying about thread safety.
    -   The function name change mimics the change in the semantics of
        the function.
    -   The various callers were modified to incorperate this change

**8 August (Fri)**

-   Optimized *ReadReal*. Replaced calls to input stream peek & get with
    judicious use of get.
-   Work done from 7 August was organized into commits and pushed to
    github.

### Week 13

**9 August (Sat)**

-   No changes were done to *Sdai\** files of the *cleditor* library as
    those files were generated by *exp2cxx*.
    -   Any modifications would be lost if *exp2cxx* was used to
        regenerate them.
-   Went through *STEPfile* class to determine the areas of thread
    safety violations.

**10 August (Sun)**

-   Inspired by a comment written by a developer, removed *istream
    \*in2* from *STEPfile::AppendFile*.
    -   Originally for the second pass a new *istream (in2)* was being
        created and the *.step* file was being opened again.
    -   The above was prevented by directing the original istream (in)
        to the beggining of the *.step* file.
    -   The work was commited and pushed into github.

**11 August (Mon)**

-   Protected *_headerId* in *STEPfile* *(cleditor)*.
    -   *_headerId* is a counter used in *STEPfile* class.
    -   Its value could change in *ReadHeader* and *ReadExchangeFile*
        methods.
    -   Hence a mutex was introduced specially to protect it.
-   Added *GetApplication_instanceFromFileId* method in *InstMgr*
    class.
    -   The *SDAI_Application_instance \* GetApplication_instance(
        MgrNode \* )* and*MgrNode \* FindFileId( int )* methods of class
        *InstMgr* were often being used together in the class
        *STEPfile*.
    -   Therefore a special function was created in class *InstMgr* of
        the form *SDAI_Application_instance \*
        GetApplication_instanceFromFileId( int )* which would take care
        of locking and consistency issues.
    -   This function was then used in *STEPfile*.

**12 August (Tue)**

-   Safe *InstMgr* iteration in *STEPfile*.
    -   Variables of class *InstMgr* were being iterated upon in class
        *STEPfile* through the variables *_instances* (including its
        get function *instances()*) and *_headerInstances*.
    -   The mtx defined in *InstMgr* was invoked to make them safe.

**13 August (Wed)**

-   Safe *attributes* iteration in *STEPfile*.
    -   This was done by using mutexes defined for
        *SDAI_Application_instance* & *SingleLinkList* classes.
-   It was decided that as this class acts like a parser, further
    locking in this class would be dependent upon how it will be used in
    a multithreaded way.
    -   The current structure of the class was restricting any potential
        multithreaded use.
    -   Example: The variable like *_fileName* restricts this class to
        parse only one file at a time. If we want to parse more then one
        then this would have to change.
-   Thread safety in *SDAI_Application_instance__set*
    -   This was done by introducing a *recursive_mutex* in the
        *SDAI_Application_instance__set* class.
-   Work done from 11 August was organized into commits and pushed to
    github.

**14 Augest (Thu)**

-   Removed compile time warning from the previous day commit.
-   Added class *SDAI__set* in *cldai* library
    -   It was noticed that some classes in this library which were very
        similar: *SDAI_DAObject__set*, *SDAI_Entity_extent__set*
        & *SDAI_Model_contents__list*
    -   The logic common to these classes was indentified and removed, a
        new class (*SDAI__set*) was created which had that common
        logic.
    -   The original classes were made to inherit from the new class.
    -   This removed duplicated code and also made making changes (for
        thread safety) easier.
-   Made *SDAI__set* thread safe
    -   This was done by introducing a mutex in the *SDAI__set* class.

**15 Augest (Fri)**

-   Added *SDAI__set::Remove( SDAI_ptr )* function
    -   The semantics of this function would be similar to
        *SDAI__set::Remove( SDAI__set::Index( SDAI_ptr ) )*. The
        only difference would be that in the new function both the
        operations are done under a single lock.
    -   Wherever the old *Remove( Index( SDAI_ptr ) )* code snippet was
        found, it was replaced by the new *Remove( SDAI_ptr )*
        function.
-   One more subclass of *SDAI__set*
    -   Adding the *Remove( SDAI_ptr )* API to *SDAI__set* made
        *SDAI_Application_instance__set* a candidate for inheriting
        common logic from *SDAI__set*.
    -   Note: This class was already made thread safe in one of the
        previous commits. This commit only removes the now apparent
        duplicate code.
-   Work done from 14 August was organized into commits and pushed to
    github.

### Week 14

**16 Augest (Sat)**

-   On the advice of *starseeker* I decided to perform the *acid test*
    by running my version of stepcode through *step-g* converter.
    -   Set up *brlcad*.
    -   Ran *step-g* converter on a sample ap203 file.

**17 Augest (Sun)**

-   Tried to run *step-g* using my stepcode version. Unfortunately I was
    not successful partially due to the following reasons.
    -   To start with, a lot of time was wasted, identifying the CMake
        file in brlcad in which I should set *CMAKE_CXX_FLAGS* (or
        equivalent) with *-std=c++0x* so as to run my version of
        stepcode which uses *std::mutex* & *std::thread*
    -   Secondly apart from the changes I did in stepcode through
        *hj/thread-safety* branch the stepcode version in
        *brlcad/src/other/stepcode* had many differences.
        -   It initially gave many build errors.
        -   When it finally ran it gave a seg-fault on the piece of code
            I have never changed.
-   Added *NO_REGISTRY* macro to *lazy_thread_safety_test*
    -   *lazy_thread_safety_test* had 2 checks which were schema
        dependent. These checks are now wrapped in *NO_REGISTRY* macro.

**18 Augest (Mon)**

-   Utilized *sc_mutex* in *cllazyfile*
    -   Earlier *std::mutex* was being used.
    -   It was replaced with *sc_mutex* which acts like a wrapper to
        *std::mutex*.
-   Added *sc_thread.h* in *clutils*
    -   The class acts like a wrapper to some of the thread
        functionalities (like *get_id()*) which is being used in
        stepcode.
    -   If the compiler does not supports thread functionalities then
        this class provides dummy types and functionalities.
    -   *instMgrAdapter* & *lazyTypes.h* were modified so as to take
        dependency on *sc_thread*.
-   As a result of above two changes *HAVE_STD_THREAD* macros were
    removed from cllazyfile library \*.cc and \*.h as classes
    *sc_thread* and *sc_mutex* internally handles the macros.
-   Added exit(success/fail) in thread-safety test
-   Organized the work done from 17 augest into commits and pushed into
    github
-   Merged remote-tracking branch *origin/master* into
    *hj/thread-safety*
    -   As I had never merged the master branch into the branch I was
        working upon ever since I started working on this project, I was
        109 commits ahead and 23 commits behind the master branch.
    -   I merged those the 23 commits into my *hj/thread-safety* branch.
        The only conflict was in *src/clstepcore/instMgr.cc* which was
        handled by me.