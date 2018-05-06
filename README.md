# `k8schain`

This is an implementation of the [github.com/google/go-containerregistry](
https://github.com/google/go-containerregistry) library's [`authn.Keychain`](
https://godoc.org/github.com/google/go-containerregistry/authn#Keychain)
interface based on the authentication semantics used by the Kubelet when
performing the pull of a Pod's images.

## Usage

The `k8schain.Default` can be used directly as an `authn.Keychain`, e.g.

```go
	// TODO(mattmoor): The interface here.
	foo := k8schain.Default()
	auth, err := foo.Resolve(registry)
	if err != nil {
		...
	}
```

Or, it can be used to override the default keychain used by this process,
which by default follows Docker's keychain semantics:

```go
func init() {
	// TODO(mattmoor): The interface here.
	foo := k8schain.Default()

	// Override the default keychain used by this process to follow the
	// Kubelet's keychain semantics.
	authn.DefaultKeychain = foo
}
```
