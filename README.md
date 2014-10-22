# µMatrix for Chromium

[Under development: usable, but persistence schema not finalized, will certainly change]

Forked from [HTTP Switchboard](https://github.com/gorhill/httpswitchboard).

Differences with HTTP Switchboard:

- No pattern-based filtering -- use more advanced [µBlock](https://github.com/gorhill/uBlock) for this
- Rules from broader scopes propagate to narrower scopes ([HTTP Switchboard issue #227](https://github.com/gorhill/httpswitchboard/issues/227)):
    - This means rules in global scope are ubiquitous, i.e. no longer sandboxed
    - See matrix as really 3D: evaluation order: Z, then X and Y, where
        - Z is the source hostname axis (aka "scope"), from narrower scopes to global scope
        - X is the request type axis: `*`, `cookie`, `css`, etc.
        - Y is the destination hostname axis (`www.example.com`, `example.com`, `com`, `*`)
    - Switching scopes in matrix popup does not create/delete scopes, this just allows a user to modify rules in a specific scope
        - Rules in narrower scope(s) still exist and are enforced even if you have the global scope selected
- Much needed [code refactoring](http://en.wikipedia.org/wiki/Code_refactoring) toward portability/efficiency
    - Big chunks of tired code have been removed, or replaced by small chunks of better code
    - There is no longer a hierarchical data structures for scopes/rules (**major** contribution toward code simplification)
    - Thus no need to manage the creation/deletion of scopes (and related settings)
    - All scopes virtually exist at all time.
    - The popup matrix simply activate whatever last scope level was in use

## License

<a href="https://github.com/gorhill/umatrix/blob/master/LICENSE.txt">GPLv3</a>.