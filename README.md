We forked this repo for us to use version 7.0.2 of this library and extend it. The problem with later versions is that the authors intentionally deprecated `autoFormat` option, which is a very important feature we need for MyCRM.

However, there was an update on NZ mobile number validation rules that is not available on v7.0.2. So we need to use those new validation rules on v7.0.2. Hence, this repo.

## UPDATING

When updating the validation rules,

- checkout `v7.0.2-h`, where `h` is an incremental alphabetic version.
- Open `lib/libphonenumber/build/utils.js` file.
- Find the country code you will be modifying and replace its configuration with the correct one.
- Commit your changes
- run `git tag v7.0.2-<next-version>`
- checkout to new tag `git checkout v7.0.2-<next-version>`
- push tag `git push origin v7.0.2-<next-version>`
- you can now use the tag in other projects, just update the tag version `"intl-tel-input": "github:loanmarket/intl-tel-input#v7.0.2-<next-version>"`
- checkout to a branch (e.g `git checkout -b fix-gh-validation`)
- update this readme to change the version (version you just tagged) then push to create a PR to develop branch

---

See [intl-tel-input](https://github.com/jackocnr/intl-tel-input) for original README.

---

## CONFIGURATION PER COUNTRY

We can find a country's configuration by searching the file `lib/libphonenumber/build/utils.js` with the country's ISO Alpha-2 code (e.g. GH for Ghana).
If the fix can't be done with simple modification of these configurations, we can try copying the updated configuration from the actual library.

When updating a country's configuration using the latest build from the library:

- Look for the latest build from [intl-tel-input](https://github.com/jackocnr/intl-tel-input) (As of writing, it can be found in src/js/utils.js)
- Find the country's configuration, try to format per array item depending on your preference (pls check GHANA in v7.0.2-g for reference)
- Notice that the latest structure/format from the copied config is different with our current build (not just the regex)
- Example:

  | Current                                | Latest from library                         |
  | -------------------------------------- | ------------------------------------------- |
  | [,,"NA","NA"]                          | [,,,,,,,,,[-1]]                             |
  | [,,"800\\d{5}","\\d{8}"]               | [,,"800\\d{5}",,,,,,,[8]]                   |
  | [,,"(?:[235]\\d{3})\\d{5}","\\d{7,9}"] | [,,"(?:[235]\\d{3})\\d{5}",,,,,,,[8,9],[7]] |

- This is because the library's parser has changed since the forking of the version we are using
- Thus the need to understand their difference to safely copy the latest patterns to our version
- Please also note that their parser may have changed since this writing so this might no longer be applicable
- Feel free to update this readme and add tips to make fixing easier for other devs
