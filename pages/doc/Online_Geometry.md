# Aim of Project

The aim of this project is to provide an online service to users of
BRL-CAD to view and share their geometric files (BRL-CAD's native .g
file) on browser. Currently in initial development stage, project aimed
to have more advanced features in near future with ultimate goal to
provide geometry editing features by leveraging BRL-CAD's existing code
to maximum extent.

# Current Implementation

### Brief workflow

JavaScript 3D library, ThreeJS is used for drawing 3D models in browser.
But ThreeJS doesn't support .g format. However, it can read obj files.
obj is plain text format that can represent 3D geometry. It stores
position of vertices, vertex normals and faces etc. You can read more
about obj at: <http://en.wikipedia.org/wiki/Wavefront_.obj_file>

BRL-CAD has converter called g-obj that simply converts specified
object(s) from BRL-CAD database .g file to obj file(s). So, right now
g-obj plays fundamental role in the working of this project but there
are lot of possibilities to replace this with some robust method.

In the end, obj file is given to ThreeJS and it draws entity on browser.

### Detailed workflow

Here is the flow diagram of OGV: [Media:
Flow_diagram_of_online_geometry_viewer.jpeg](Media:_Flow_diagram_of_online_geometry_viewer.jpeg.md).
We can divide the whole process in following four operations:

-   Upload .g file
-   Extracting data
-   Conversion
-   Display

Above four operations are performed by following four files:

|                         |                                                                                                                                                                                           |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **upload.php:**         | It provides a web interface for user to upload .g file.                                                                                                                                   |
| **upload_file.php:**   | It extracts data that includes name of .g file and that of its entities and pass it to model_display.php.                                                                                |
| **model_display.php:** | It provides list of entities for user to choose from. When user clicks the "view" button corresponding to any entity, request is sent to create_obj.php for creating obj file.           |
| **create_obj.php:**    | As name suggests, when request received from model_display.php, it run g-obj converter that creates obj and respond with appropriate status. If success, entity is displayed on browser. |

#### Extracting name of .g file and that of its entities:

Name of file is extracted using PHP's $_FILES variable and list of
entities of .g file are copied to PHP variable using BRL-CAD's "ls"
command.

#### Conversion

When .g file is uploaded, user is redirected to model_display.php. When
user clicks on "view", add_entitiy() method is called that sends an
AJAX request to create_obj.php. In create_obj.php, create_obj()
method runs g.obj converter that creates obj file.

#### Languages used

|                |       |
|----------------|-------|
| **PHP**        | 74.3% |
| **CSS**        | 13.6% |
| **JavaScript** | 12.1% |

#### Third party libraries

|                   |                                       |
|-------------------|---------------------------------------|
| **ThreeJS:**      | 3D JavaScript webGL library           |
| **BootStrap:**    | Front-end framework used for CSS work |
| **pace.js:**      | Automatic page load progress bar      |
| **jquery:**       | For AJAX work                         |
| **Swift Mailer:** | For sending emails                    |

#### Top level directories

|                     |                                        |
|---------------------|----------------------------------------|
| **accounts:**       | Sign-in signup module, swift mailer    |
| **css:**            | images, pace.js                        |
| **doc:**            | html, latex                            |
| **images**          |                                        |
| **js:**             | ThreeJS                                |
| **user_accounts:** | Parent directory for user directories. |

#### Other files

|                      |                                                                                                                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **config.php:**      | A global configuration file.                                                                                                                                                    |
| **doxyfile:**        | Doxygen file.                                                                                                                                                                   |
| **functions.php:**   | PHP functions                                                                                                                                                                   |
| **geo_viewer.sql:** | Database schema file (.sql)                                                                                                                                                     |
| **header.php:**      | Common file for header of webpage. (TODO: There are two header.php files, one in root directory and other in accounts/include. One of these duplicate files need to be removed) |
| **README.md**        |                                                                                                                                                                                 |
| **variables.php:**   | Contain variables.                                                                                                                                                              |

Further, detailed comments are written in the source code itself. If you
still have doubts, questions etc., please contact at
brlcad-devel@lists.sourceforge.net or at IRC at \#brlcad channel on
freenode network.

# Status of Development

See the [TODO](Online_Geometry/TODO.md) page to get involved or
check on the status of development.

# History

This effort was initiated in 2013 by Harmanpreet Singh as a Google
Summer of Code project.
