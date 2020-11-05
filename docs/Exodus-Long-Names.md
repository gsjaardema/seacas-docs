On write, you can call:

   ```
   ex_set_option(exoid, EX_OPT_MAX_NAME_LENGTH, {max_name_length});
   ```

 or equivalently

   ```
   ex_set_max_name_length(exoid, {max_name_length});
   ```

which tells the database that you will be using names of that length or shorter.

This same call on read will tell the database to truncate names at
that length. If not called, then the `{max_name_length}` is assumed to
be 32 characters which has been the historic maximum name length for
exodus.

Following this call, you can define (i.e., read/write) names of any
size; if the names are longer than `{max_name_length}`, then they will be truncated otherwise they will pass through unchanged.

There are three queries that can be made to `ex_inquire` or
`ex_inquire_int`: 

* `EX_INQ_DB_MAX_ALLOWED_NAME_LENGTH` -- returns the value of the
  maximum size that can be specified for `max_name_length`
  (netcdf/hdf5 limitation)
* `EX_INQ_DB_MAX_USED_NAME_LENGTH` -- returns the size of the longest
  name on the database.
* `EX_INQ_MAX_READ_NAME_LENGTH` -- returns the maximum name length
  size that will be passed back to the client. 32 by default,
  set by the previously mentioned `ex_set_option()` or
  `ex_set_max_name_length()` call.
  
The length of the QA records is not affected by this setting and each entry in the QA record is still limited to 32 characters.
