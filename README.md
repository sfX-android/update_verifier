# Install

```
git clone https://github.com/sfX-Android/update_verifier
cd update_verifier

# legacy (won't work on modern distributions):
pip install -r requirements.txt

# modern approach
python -m venv ~/.venvs/updateverifier
~/.venvs/updateverifier/bin/pip install -r requirements.txt
```

# Usage

## Verifying Build Authenticity

You can verify whether a build has been signed with our keys with this command:

```
# when not using a venv:
python update_verifier.py <AXP.OS|EOS|LOS>/XXX_pubkey /path/to/zip`

# when using a venv:
`~/.venvs/updateverifier/bin/python update_verifier.py <AXP.OS|EOS|LOS>/XXX_pubkey /path/to/zip

# (obviously replace "<AXP.OS|EOS|LOS>/XXX_pubkey" with the real public key file
# and "/path/to/zip" with the path to the zip you want to verify)
```

If the script reports **verified successfully**, the ZIP file signature is valid and matching the given key.

## The public known AOSP testkey

If an OS ZIP is **not** signed with a custom key it will get still signed by the public known AOSP testkey (see [here](https://cs.android.com/android/platform/superproject/+/main:build/make/tools/releasetools/testdata/testkey.key)).

But: the private part of that testkey is known to *everyone* and so **cannot** be trusted!

So everyone can modify the ZIP and re-sign it with that known testkey and your recovery and/or OS will accept it (if not configured otherwise).

So if the following command succeeds for the ZIP tested it means you should never trust it:

`python update_verifier.py AOSP_TESTKEY_pubkey /path/to/zip`

If it says: "failed" you are good as it means the ZIP was **not** signed by the testkey.
