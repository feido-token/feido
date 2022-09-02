# FeIDo: Recoverable FIDO2 Tokens Using Electronic IDs
This is the umbrella repository of the FeIDo research project.
The corresponding paper has been accepted for CCS 2022 and will be published as part of the proceedings.


## Directory structure
* `feido-middleware-app/`       -- FeIDo's client middleware as an Android app

* `feido-browser-extension/`    -- FeIDo's (client-side) browser extension for Firefox

* `feido-database-server/`      -- demo eID revocation database service (mimicking Interpol's I-Checkit)

* `feido-credential-service/`   -- FeIDo's Credential Service implemented using Intel SGX as the TEE

* `protobuf/`                   -- protobuf files for inter-component communication

* `webauthn/`                   -- small patch to webauthn.io for the performance evaluation



## Build and Run Instructions Overview
In the following, we will provide an overview of the steps required to build an
run the FeIDo prototype.
Please refer to the README files of each subcomponent for detailed build and run
instructions of the respective FeIDo subcomponent.

1. Initialize and update all submodules:
    ```
    git submodule update --init
    ```


2. Build the Middleware Android app by following the instructions given in `feido-middleware-app/README.md`.

    Then run it on a connected smartphone *with NFC support*.
    The current protoype has been successfully tested on a `Samsung Galaxy S8` running `Android 9 (Pie)`.


3. Prepare and install the Firefox Browser extension by following the instruction given in `feido-browser-extension/README-md`.


4. Prepare, configure, and build the Intel SGX Credential Service:

    Follow the build instructions given in `feido-credential-service/README.md`.
    Then run the `credservice-sgx` executable (also see specific README file).

5. Configure, build, and run the demo eID Revocation Database Service:

    Follow the build and run instructions given in `feido-database-server/README.md`.

6. Optionally: Follow the instructions in `webauthn/` to host the webauthn.io page
    locally (with time measurement patch).


7. Connect the Android app (FeIDo middleware) with your German ePassport:

    Input your ePassport's MRZ data into the Android app.
    Place your phone on to your ePassport to connect to it via NFC.
    When using a Galaxy S8, you put the whole phone centrally on your ePassport
    (i.e., the phone covers the whole ePassport).
    On success, the phone will vibrate and connect to your ePassport (check the
    log messages given in the status field of the app).

    The current prototype supports *only German ePassports* at the moment.


8. Perform the registration and login with your Firefox browser.

    Using your Firefox browser with loaded FeIDo extension, navigate to `webauthn.io`
    (or your locally hosted instance of it).
    Input a user name and hit `Register`.
    Wait for the output console in the Android app to stop, then hit `Login`.
    You should now be redirected to a "successful login" page.

    Warning: if hosting webautn.io locally, connect via `localhost`, not via IP
    (127.0.0.1), as this will currently cause a name mismatch error, shown in the
    webauthn.io log as:
    ```
    Expected: "localhost"
    Received: "127.0.0.1"
    ```



## License
The FeIDo source code will be openly licensed, but is currently still under restrictive/no license.
The exact open source license still needs to be determined and might vary across
the different subcomponents.
