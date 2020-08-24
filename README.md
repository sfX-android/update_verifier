# Install

```
git clone https://github.com/LineageOS/update_verifier
cd update_verifier
pip install -r requirements.txt
```

# Usage

## Verifying Build Authenticity

You can verify whether a build has been signed with our keys with this command:

`python update_verifier.py lineageos_pubkey /path/to/zip`

If the script reports **verified successfully**, the ZIP file signature is valid.

For the paranoid, the contents of this page are stored on our GitHub.
