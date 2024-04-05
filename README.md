# Install

```
git clone https://github.com/sfX-Android/update_verifier
cd update_verifier
pip install -r requirements.txt
```

# Usage

## Verifying Build Authenticity

You can verify whether a build has been signed with our keys with this command:

`python update_verifier.py XXX_pubkey /path/to/zip`

(obviously replace *XXX_pubkey* with the public key file and */path/to/zip* with the path to the zip you want to verify)

If the script reports **verified successfully**, the ZIP file signature is valid.

For the paranoid, the contents of this page are stored on our GitHub.

## The public known AOSP testkey

If an OS ZIP is **not** signed with a custom key it will get still signed by the public known AOSP testkey (see [here](https://cs.android.com/android/platform/superproject/+/main:build/make/tools/releasetools/testdata/testkey.key)).

But: the private part of that testkey is known to *everyone* and so **cannot** be trusted!

So everyone can modify the ZIP and re-sign it with that known testkey and your recovery and/or OS will accept it (if not configured otherwise).

So if the following command succeeds for the ZIP tested it means you should never trust it:

`python update_verifier.py AOSP_TESTKEY_pubkey /path/to/zip`

If it says: "failed" you are good as it means the ZIP was **not** signed by the testkey.
