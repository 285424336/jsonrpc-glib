# Contributing to Jsonrpc-GLib

## Licensing

Your work is considered a derivative work of the jsonrpc-glib codebase and therefore must be licensed as LGPLv2.1+ to be included in our code-base.
You may optionally grant other licensing in addition to LGPLv2.1+ such as Apache 2.0 or MIT X11.
However, as part of Jsonrpc-GLib, the combined work will be LGPLv2.1+.

You do not need to assign us copyright attribution.
It is our belief that you should always retain copyright on your own work.

## Testing

When working on a new feature or bug fix, try to write a new test or adjust an existing test to cover your use case.
Not everything we have in the code base has tests, and ideally that will improve, not get worse.

## Code Style

We follow the GObject and Gtk coding style.
That is often unfamiliar to those who have not been hacking on GNU projects for the past couple of decades.
However, it is largely entrenched in our community, so we try to be consistent.

```c
static gboolean
this_is_a_function (GtkWidget    *param,
                    const gchar  *another_param,
                    guint         third_param,
                    GError      **error)
{
  g_return_val_if_fail (GTK_IS_WIDGET (param), FALSE);
  g_return_val_if_fail (third_param > 10, FALSE);

  if (another_param != NULL)
    {
      if (!do_some_more_work ())
        {
          g_set_error (error,
                       G_IO_ERROR,
                       G_IO_ERROR_FAILED,
                       "Something failed");
          return FALSE;
        }
    }

goto_labels_here:

  return TRUE;
}
```

```c
void      do_something_one   (GtkWidget  *widget);
void      do_something_two   (GtkWidget  *widget,
                              GError    **error);
gchar    *do_something_three (GtkWidget  *widget);
gboolean  do_something_four  (GtkWidget  *widget);
```

 * Notice that we use 2-space indention.
 * We indent new blocks {} with 2 spaces, and braces on their own line. We understand that this is confusing at first, but it is rather nice once it becomes familiar.
 * No tabs, spaces only.
 * Always compare against `NULL` rather than implicit comparisons. This eases ports to other languages and readability.
 * Use #define for constants. Try to avoid "magic constants".
 * goto labels are fully unindented.
 * Align function parameters.
 * Align blocks of function declarations in the header. This vastly improves readability and scanning to find what you want.

If in doubt, look for examples elsewhere in the codebase.

