[category:Code examples](category:Code_examples.md)

`#include <brlcad/MemoryDatabase.h>`

`#include <brlcad/Halfspace.h>`
`#include <brlcad/Combination.h>`


`int main`
`(`
`    int   argc,`
`    char* argv[]`
`) {`
`    BRLCAD::Halfspace halfspace;`
`    halfspace.SetName("half.s");`
`    halfspace.SetNormal(BRLCAD::Vector3D(1., 1., 1.));`
`    halfspace.SetDistanceFromOrigin(1500.);`

`    BRLCAD::Combination region;`
`    region.SetName("half.r");`
`    region.SetIsRegion(true);`
`    region.AddLeaf("half.s");`

`    BRLCAD::Combination group;`
`    group.SetName("all.g");`
`    group.AddLeaf("half.r");`

`    BRLCAD::MemoryDatabase database;`
`    database.Add(halfspace);`
`    database.Add(region);`
`    database.Add(group);`
`    database.Save("my-db.g");`

`    return 0;`
`}`
