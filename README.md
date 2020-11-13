
We forked this repo for us to use version 7.0.2 of this library and extend it. The problem with later versions is that the suthors intentionally deprecated `autoFormat` option, which is a very important feature we need for MyCRM.

However, there was an update on NZ mobile number validation rules that is not available on v7.0.2. So we need to use those new validation rules on v7.0.2. Hence, this repo.

## UPDATING

When updating the validation rules, 

* checkout `v7.0.2-h`, where `h` is an incremental alphabetic version. 
* Open `lib/libphonenumber/build/utils.js` file.
* Find the country code you will be modifying and replace its configuration with the correct one.
* Commit your changes
* run `git tag v7.0.2-<next-version>`
* update this readme to change the version (version you just tagged) on checkout step.
* push


***

See [intl-tel-input](https://github.com/jackocnr/intl-tel-input) for original README.
