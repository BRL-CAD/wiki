## Introduction

This tutorial will demonstrate the process of integrating conversion
plugins into the Geometry Conversion Library (GCV).

## Build Integration

In order to associate the plugin with a file format, an associated MIME
type must be present in `enum mime_model_t`, located within
`include/bu/mime.h`. This enum is generated from `misc/mime_cad.types`,
so we will add an entry there:

`model/foomodel foo`

Now we will create a source file for our plugin. For now, it will be an
empty file:

`mkdir src/libgcv/conv/foomodel`
`touch src/libgcv/conv/foomodel/foomodel_write.c`

Next, add this file path to `LIBGCV_CONVERTER_SOURCES` within
`src/libgcv/CMakeLists.txt`.

Now we will register the converter. Add the following line to
`gcv_get_converters()` within `src/libgcv/plugin.c`. We will define the
named symbol later.

`CONVERTER(gcv_conv_foomodel_write);`

## Plugin Implementation

We are now ready to implement the plugin. Below is potential code for
for `foomodel_write.c`.

`#include "common.h"`

`#include "../plugin.h"`


`struct gcv_foomodel_options_data {`
`    int max_objects;`
`    int starting_id;`
`};`


`HIDDEN int`
`gcv_foomodel_write(const char *dest_path,`
`                   struct db_i *UNUSED(source_dbip),`
`                   const struct gcv_opts *UNUSED(gcv_options),`
`                   const void *options_data)`
`{`
`    const struct gcv_foomodel_options_data *options =`
`        (struct gcv_foomodel_options_data *)options_data;`

`    bu_log("writing foomodel to '%s'\n", dest_path);`
`    bu_log("max_objects = %d\n", options->max_objects);`
`    bu_log("starting_id = %d\n", options->starting_id);`

`    if (max_objects < 0 || starting_id < 0) {`
`        bu_log("invalid value\n");`
`        return 0;`
`    }`

`    /* success */`
`    return 1;`
`}`


`HIDDEN void`
`gcv_foomodel_create_opts(struct bu_opt_desc **options_desc,`
`                         void **dest_options_data)`
`{`
`    struct gcv_foomodel_options_data *options_data =`
`        (struct gcv_foomodel_options_data *)`
`        bu_malloc(sizeof(struct gcv_foomodel_options_data), "options_data");`

`    *dest_options_data = options_data;`

`    *options_desc = (struct bu_opt_desc *)`
`        bu_malloc(3 * sizeof(struct bu_opt_desc), "options_desc");`

`    BU_OPT((*options_desc)[0], "m", "max-objects", NULL, bu_opt_int,`
`           &options_data->max_objects, "max number of objects to create");`

`    BU_OPT((*options_desc)[1], "i", "starting-id", "id", bu_opt_int,`
`          &options_data->starting_id, "starting object ID");`

`    BU_OPT_NULL((*options_desc)[2]);`

`    /* initialize defaults */`
`    options_data->max_objects = 0;`
`    options_data->starting_id = 0;`
`}`


`HIDDEN void`
`gcv_foomodel_free_opts(void *options_data)`
`{`
`    bu_free(options_data, "options_data");`
`}`


`/* plugin information */`
`const struct gcv_converter gcv_conv_foomodel_write = {`
`    MIME_MODEL_FOOMODEL,`
`    GCV_CONVERSION_WRITE,`
`    gcv_foomodel_create_opts,`
`    gcv_foomodel_free_opts,`
`    gcv_foomodel_write`
`};`