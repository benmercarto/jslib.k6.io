# jslib.k6.io

Remote utility JS libs for k6 scripts.


## Installing new package via npm and automagically adding it to libs
The outcome of this might vary depeding on the quality of the desired node_module you want to add.

The following command will try to:
1. Install the desired {package_name}
2. Copy the module to `/lib`
3. Update the homepage `/lib/index.html`

```bash
yarn run add-pkg {package_name}
```

Once run successfully, make sure that you do the following:
- Add test case in `/tests/basic.js` to make sure that the ported lib is importable and runnable by k6.
- Verify that new homepage `/lib/index.html` is legit.


## How to add a new lib
1. Create a new lib dir `/lib/{lib_name}`
3. Create a new version dir `/lib/{lib_name}/{desired_version}/`
4. Add entry file version `/lib/{lib_name}/{desired_version}/{desired_name}.js`
5. Add the lib to `supported.json` like:
```javascript
{
  "{lib_name}": {
    "{desired_version}": {}
  }
}

// Example result
{
  "awesome-lib": {
    "2.0.3": {}
  }
}
```
6. Add test case in `/tests/basic.js` to make sure that the ported lib is importable and runnable by k6.
7. Update the homepage by running `yarn run generate-homepage`.
8. Verify that new homepage `/lib/index.html` is legit (Quickly done by running `yarn run verify-homepage`).
9. Merge master.
10. Browse to https://jslib.k6.io/{lib_name}/{desired_version}/{desired_name}.js

## How to add a new version of a and existing lib
1. Create a new "version dir" in `/lib/{lib_name}/{desired_version}/`
2. Add entry file for version `/lib/{lib_name}/{desired_version}/{desired_name}.js`
3. Add the version to `supported.json` like:
```javascript
{
  "my-lib": {
    "1.0.2": {},
    // Use semantic versioning
    "{desired_version}": {}
  }
}

// Example result
{
  "my-lib": {
    "1.0.2": {},
    "2.0.3": {}
  }
}
```
4. Add test case in `/tests/basic.js` to make sure that the ported lib is importable and runnable by k6.
5. Update the homepage by running `yarn run generate-homepage`.
6. Verify that new homepage `/lib/index.html` is legit (Quickly done by running `yarn run verify-homepage`).
7. Merge master.
8. Browse to https://jslib.k6.io/{lib_name}/{desired_version}/{desired_name}.js


## Updating styling and layout of the "Homepage"

The homepage of https://jslib.k6.io live in the `/static` dir.\
The final `index.html` page gets generated by running `yarn run generate-homepage`.

Useful dev commands:

```bash
# Listen to file changes, restart devserver and serve index.html
yarn run develop-homepage

# Quickly serve index.html
yarn run verify-homepage

# Generate index.html
yarn run generate-homepage
```