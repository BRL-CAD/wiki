[category:Code examples](category:Code_examples.md)

`#include `<iostream>
`#include `<string>

`#include <brlcad/ConstDatabase.h>`
`#include <brlcad/Combination.h>`


`class CombinationsCb;`


`void ListTreeNode(const BRLCAD::Combination::ConstTreeNode& node,`
`                  const BRLCAD::ConstDatabase&              database,`
`                  CombinationsCb&                           callback);`


`class CombinationsCb : public BRLCAD::ConstDatabase::ObjectCallback {`
`public:`
`    CombinationsCb(const BRLCAD::ConstDatabase& database) : BRLCAD::ConstDatabase::ObjectCallback(),`
`                                                            m_database(database),`
`                                                            m_prefix() {}`

`    CombinationsCb(const BRLCAD::ConstDatabase& database,`
`                   const std::string&           prefix) : BRLCAD::ConstDatabase::ObjectCallback(),`
`                                                          m_database(database),`
`                                                          m_prefix(prefix) {}`

`    void         Print(const char* name) {`
`        std::cout << m_prefix << name << std::endl;`
`    }`

`    virtual void operator()(const BRLCAD::Object& object) {`
`        const BRLCAD::Combination* comb = dynamic_cast<const BRLCAD::Combination*>(&object);`

`        if (comb != 0)`
`            ListTreeNode(comb->Tree(), m_database, CombinationsCb(m_database, m_prefix + '\t'));`
`    }`

`private:`
`    const BRLCAD::ConstDatabase& m_database;`
`    std::string                  m_prefix;`
`};`


`void ListTreeNode`
`(`
`    const BRLCAD::Combination::ConstTreeNode& node,`
`    const BRLCAD::ConstDatabase&              database,`
`    CombinationsCb&                           callback`
`) {`
`    switch (node.Operation()) {`
`        case BRLCAD::Combination::ConstTreeNode::Union:`
`        case BRLCAD::Combination::ConstTreeNode::Intersection:`
`        case BRLCAD::Combination::ConstTreeNode::Subtraction:`
`        case BRLCAD::Combination::ConstTreeNode::ExclusiveOr:`
`            ListTreeNode(node.LeftOperand(), database, callback);`
`            ListTreeNode(node.RightOperand(), database, callback);`
`            break;`

`        case BRLCAD::Combination::ConstTreeNode::Not:`
`            ListTreeNode(node.Operand(), database, callback);`
`            break;`

`        case BRLCAD::Combination::ConstTreeNode::Leaf:`
`            callback.Print(node.Name());`
`            database.Get(node.Name(), callback);`
`    }`
`}`


`int main`
`(`
`    int   argc,`
`    char* argv[]`
`) {`
`    int ret = 0;`

`    if (argc < 2) {`
`        std::cout << "Usage: " << argv[0] << " `<BRL-CAD Database>`" << std::endl;`
`        ret = 1;`
`    }`
`    else {`
`        BRLCAD::ConstDatabase database;`

`        if (database.Load(argv[1])) {`
`            BRLCAD::ConstDatabase::TopObjectIterator it = database.FirstTopObject();`
`            CombinationsCb                           callback(database);`

`            while (it.Good()) {`
`                std::cout << it.Name() << std::endl;`
`                database.Get(it.Name(), callback);`
`                ++it;`
`            }`
`        }`
`        else`
`            ret = 2;`
`    }`

`    return ret;`
`}`
