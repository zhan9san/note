# Docker Shell VS Exec

The `CMD` instruction has three forms:

* `CMD ["executable","param1","param2"]` (exec form, this is the preferred form)
* `CMD ["param1","param2"]` (as default parameters to ENTRYPOINT)
* `CMD command param1 param2` (shell form)

There can only be one `CMD` instruction in a `Dockerfile`. If you list more than one `CMD` then only the last `CMD` will take effect.

**The main purpose of a `CMD` is to provide defaults for an executing container**. These defaults can include an executable, or they can omit the executable, in which case you must specify an `ENTRYPOINT` instruction as well.

If `CMD` is used to provide default arguments for the `ENTRYPOINT` instruction, both the `CMD` and `ENTRYPOINT` instructions should be specified with the JSON array format.

**Note**

The exec form is parsed as a JSON array, which means that you must use double-quotes (“) around words not single-quotes (‘).

Unlike the shell form, the exec form does not invoke a command shell. This means that normal shell processing does not happen. For example, `CMD [ "echo", "$HOME" ]` will not do variable substitution on `$HOME`. If you want shell processing then either use the shell form or execute a shell directly, for example: `CMD [ "sh", "-c", "echo $HOME" ]`. When using the exec form and executing a shell directly, as in the case for the shell form, it is the shell that is doing the environment variable expansion, not docker.

If you use the shell form of the `CMD`, then the `<command>` will execute in `/bin/sh -c`:

    ```Dockerfile
    FROM ubuntu
    CMD echo "This is a test." | wc -
    ```

If you want to run your `<command>` without a shell then you must express the command as a JSON array and give the full path to the executable. **This array form is the preferred format of** `CMD`. Any additional parameters must be individually expressed as strings in the array:

    ```Dockerfile
    FROM ubuntu
    CMD ["/usr/bin/wc","--help"]
    ```

`https://docs.docker.com/engine/reference/builder/#run`
