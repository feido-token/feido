# Self-hosting webauthn.io
Use the following steps to self-host webauthn.io with patches for measuring the
authentication time.

```
# Clone and patch the repo
git clone https://github.com/duo-labs/webauthn.io.git`
cd webauthn.io
patch -p1 < ../webauthn.patch

# Build the Docker container
docker build -t webauthn.io .

# Run on 0.0.0.0:9005 (default). Connect via localhost:9005.
docker run --rm -p 9005:9005 webauthn.io
```