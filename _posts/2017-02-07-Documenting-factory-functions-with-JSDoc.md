I found it a little tricky to document a nodejs module that acts a a factory function.
The solution for me was found on a github issue [here](https://github.com/jsdoc3/jsdoc/issues/1086).
The solution is a little strange. You mark the `@returns` value of the factory function with the name of the
module.

## Example:

```javascript
/**
 * @module main/cmds
 */

/**
 * Generate a commands object
 * @param {BufferHellpers} pb - Initialized bufferhelpers
 * @returns {main/cmds} // IMPORTANT! The factory function returns the name of the module.
 */
module.exports = (config) => { // eslint-disable-line
  // Code goes here
}
```
