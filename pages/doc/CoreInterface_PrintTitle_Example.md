[category:Code examples](category:Code_examples.md)

`#include `<iostream>

`#include <brlcad/ConstDatabase.h>`


`int main`
`(`
`    int   argc,`
`    char* argv[]`
`) {`
`    int ret = 0;`

`    if (argc < 2) {`
`        std::cout << "Usage: " << argv[0] << " `<BRL-CAD Database>`";`
`        ret = 1;`
`    }`
`    else {`
`        try {`
`            BRLCAD::ConstDatabase database;`

`            if (database.Load(argv[1]))`
`                std::cout << database.Title();`
`            else {`
`                std::cout << "Could not load file: " << argv[1];`
`                ret = 2;`
`            }`
`        }`
`        catch(BRLCAD::bad_alloc& e) {`
`            std::cout << "Out of memory in: " << e.what();`
`            ret = 3;`
`        }`
`    }`

`    return ret;`
`}`
