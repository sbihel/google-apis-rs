<!---
DO NOT EDIT !
This file was generated automatically from 'src/mako/api/README.md.mako'
DO NOT EDIT !
-->
The `google-clouduseraccountsvm_beta` library allows access to all features of the *Google Cloud User Accounts* service.

This documentation was generated from *Cloud User Accounts* crate version *0.1.10+20150924*, where *20150924* is the exact revision of the *clouduseraccounts:vm_beta* schema built by the [mako](http://www.makotemplates.org/) code generator *v0.1.10*.

Everything else about the *Cloud User Accounts* *vm_beta* API can be found at the
[official documentation site](https://cloud.google.com/compute/docs/access/user-accounts/api/latest/).
# Features

Handle the following *Resources* with ease from the central [hub](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.CloudUserAccounts.html) ... 

* global accounts operations
 * [*delete*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GlobalAccountsOperationDeleteCall.html), [*get*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GlobalAccountsOperationGetCall.html) and [*list*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GlobalAccountsOperationListCall.html)
* [groups](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.Group.html)
 * [*add member*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GroupAddMemberCall.html), [*delete*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GroupDeleteCall.html), [*get*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GroupGetCall.html), [*insert*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GroupInsertCall.html), [*list*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GroupListCall.html) and [*remove member*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.GroupRemoveMemberCall.html)
* linux
 * [*get authorized keys view*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.LinuxGetAuthorizedKeysViewCall.html) and [*get linux account views*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.LinuxGetLinuxAccountViewCall.html)
* [users](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.User.html)
 * [*add public key*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.UserAddPublicKeyCall.html), [*delete*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.UserDeleteCall.html), [*get*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.UserGetCall.html), [*insert*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.UserInsertCall.html), [*list*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.UserListCall.html) and [*remove public key*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.UserRemovePublicKeyCall.html)




# Structure of this Library

The API is structured into the following primary items:

* **[Hub](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/struct.CloudUserAccounts.html)**
    * a central object to maintain state and allow accessing all *Activities*
    * creates [*Method Builders*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.MethodsBuilder.html) which in turn
      allow access to individual [*Call Builders*](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.CallBuilder.html)
* **[Resources](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.Resource.html)**
    * primary types that you can apply *Activities* to
    * a collection of properties and *Parts*
    * **[Parts](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.Part.html)**
        * a collection of properties
        * never directly used in *Activities*
* **[Activities](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.CallBuilder.html)**
    * operations to apply to *Resources*

All *structures* are marked with applicable traits to further categorize them and ease browsing.

Generally speaking, you can invoke *Activities* like this:

```Rust,ignore
let r = hub.resource().activity(...).doit()
```

Or specifically ...

```ignore
let r = hub.groups().delete(...).doit()
let r = hub.users().add_public_key(...).doit()
let r = hub.users().insert(...).doit()
let r = hub.groups().add_member(...).doit()
let r = hub.users().delete(...).doit()
let r = hub.users().remove_public_key(...).doit()
let r = hub.groups().insert(...).doit()
let r = hub.global_accounts_operations().get(...).doit()
let r = hub.groups().remove_member(...).doit()
```

The `resource()` and `activity(...)` calls create [builders][builder-pattern]. The second one dealing with `Activities` 
supports various methods to configure the impending operation (not shown here). It is made such that all required arguments have to be 
specified right away (i.e. `(...)`), whereas all optional ones can be [build up][builder-pattern] as desired.
The `doit()` method performs the actual communication with the server and returns the respective result.

# Usage

## Setting up your Project

To use this library, you would put the following lines into your `Cargo.toml` file:

```toml
[dependencies]
google-clouduseraccountsvm_beta = "*"
```

## A complete example

```Rust
extern crate hyper;
extern crate yup_oauth2 as oauth2;
extern crate google_clouduseraccountsvm_beta as clouduseraccountsvm_beta;
use clouduseraccountsvm_beta::PublicKey;
use clouduseraccountsvm_beta::{Result, Error};
use std::default::Default;
use oauth2::{Authenticator, DefaultAuthenticatorDelegate, ApplicationSecret, MemoryStorage};
use clouduseraccountsvm_beta::CloudUserAccounts;

// Get an ApplicationSecret instance by some means. It contains the `client_id` and 
// `client_secret`, among other things.
let secret: ApplicationSecret = Default::default();
// Instantiate the authenticator. It will choose a suitable authentication flow for you, 
// unless you replace  `None` with the desired Flow.
// Provide your own `AuthenticatorDelegate` to adjust the way it operates and get feedback about 
// what's going on. You probably want to bring in your own `TokenStorage` to persist tokens and
// retrieve them from storage.
let auth = Authenticator::new(&secret, DefaultAuthenticatorDelegate,
                              hyper::Client::new(),
                              <MemoryStorage as Default>::default(), None);
let mut hub = CloudUserAccounts::new(hyper::Client::new(), auth);
// As the method needs a request, you would usually fill it with the desired information
// into the respective structure. Some of the parts shown here might not be applicable !
// Values shown here are possibly random and not representative !
let mut req = PublicKey::default();

// You can configure optional parameters by calling the respective setters at will, and
// execute the final call using `doit()`.
// Values shown here are possibly random and not representative !
let result = hub.users().add_public_key(req, "project", "user")
             .doit();

match result {
    Err(e) => match e {
        // The Error enum provides details about what exactly happened.
        // You can also just use its `Debug`, `Display` or `Error` traits
         Error::HttpError(_)
        |Error::MissingAPIKey
        |Error::MissingToken(_)
        |Error::Cancelled
        |Error::UploadSizeLimitExceeded(_, _)
        |Error::Failure(_)
        |Error::BadRequest(_)
        |Error::FieldClash(_)
        |Error::JsonDecodeError(_, _) => println!("{}", e),
    },
    Ok(res) => println!("Success: {:?}", res),
}

```
## Handling Errors

All errors produced by the system are provided either as [Result](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/enum.Result.html) enumeration as return value of 
the doit() methods, or handed as possibly intermediate results to either the 
[Hub Delegate](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.Delegate.html), or the [Authenticator Delegate](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/../yup-oauth2/trait.AuthenticatorDelegate.html).

When delegates handle errors or intermediate values, they may have a chance to instruct the system to retry. This 
makes the system potentially resilient to all kinds of errors.

## Uploads and Downloads
If a method supports downloads, the response body, which is part of the [Result](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/enum.Result.html), should be
read by you to obtain the media.
If such a method also supports a [Response Result](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.ResponseResult.html), it will return that by default.
You can see it as meta-data for the actual media. To trigger a media download, you will have to set up the builder by making
this call: `.param("alt", "media")`.

Methods supporting uploads can do so using up to 2 different protocols: 
*simple* and *resumable*. The distinctiveness of each is represented by customized 
`doit(...)` methods, which are then named `upload(...)` and `upload_resumable(...)` respectively.

## Customization and Callbacks

You may alter the way an `doit()` method is called by providing a [delegate](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.Delegate.html) to the 
[Method Builder](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.CallBuilder.html) before making the final `doit()` call. 
Respective methods will be called to provide progress information, as well as determine whether the system should 
retry on failure.

The [delegate trait](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.Delegate.html) is default-implemented, allowing you to customize it with minimal effort.

## Optional Parts in Server-Requests

All structures provided by this library are made to be [enocodable](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.RequestValue.html) and 
[decodable](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.ResponseResult.html) via *json*. Optionals are used to indicate that partial requests are responses 
are valid.
Most optionals are are considered [Parts](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.Part.html) which are identifiable by name, which will be sent to 
the server to indicate either the set parts of the request or the desired parts in the response.

## Builder Arguments

Using [method builders](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.CallBuilder.html), you are able to prepare an action call by repeatedly calling it's methods.
These will always take a single argument, for which the following statements are true.

* [PODs][wiki-pod] are handed by copy
* strings are passed as `&str`
* [request values](http://byron.github.io/google-apis-rs/google_clouduseraccountsvm_beta/trait.RequestValue.html) are moved

Arguments will always be copied or cloned into the builder, to make them independent of their original life times.

[wiki-pod]: http://en.wikipedia.org/wiki/Plain_old_data_structure
[builder-pattern]: http://en.wikipedia.org/wiki/Builder_pattern
[google-go-api]: https://github.com/google/google-api-go-client

# License
The **clouduseraccountsvm_beta** library was generated by Sebastian Thiel, and is placed 
under the *MIT* license.
You can read the full text at the repository's [license file][repo-license].

[repo-license]: https://github.com/Byron/google-apis-rs/LICENSE.md