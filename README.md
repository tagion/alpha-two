<a href="https://tagion.org"><img alt="tagion logo" src="https://github.com/tagion/resources/raw/master/branding/logomark.svg?sanitize=true" alt="tagion.org" height="60"></a>

# Tagion AlphaTwo Release

> The Tagion network decentralizes trading and transferring between compatible cryptocurrencies and is operated by a democratic governance mechanism: the users of the network essentially own and control the network, as it is open and technically accessible for everyone.
> 
> The network itself consists of a **gossip protocol,** which is used for data synchronization, the **hashgraph algorithm**, which provides consensus and ordering transactions, and the **sharding** **opportunity,** which lets transactions run in parallel and enhances the speed of the system.

**AlphaTwo** is Tagion's is an improved version of the **AlphaOne**. Primarly concerning the tagion core **tagionwave**.[See AlphaOne](https://github.com/tagion/alpha_one)

See the [Release note here](RELEASE.md).



Inside the bin directory **tagionwave** core program can found.

In the current version the tagionwave has only been tested in an internal-mode this means that this is uses interprocess communication and not libp2p an in the **AlphaOne**. 

A simple test can be started as follows.

```bash
cd bin
mkdir data # Create a director for the data base
export GODEBUG=cgocheck=0
./tagionwave -N 11 --loops 1000
```

This we start 11 nodes and run 1000 iterations.

The test program we dump a logfile in **/tmp/tagion.log**



# Repository

## Maintainers

- [@cbleser](https://github.com/cbleser)
- [@alexSushko](https://github.com/alexSushko)
- [@vladpazych](https://github.com/vladpazych) (Documentation)
- [@James-at-Tagion](https://github.com/James-at-Tagion) (Documentation)

## Questions

For questions and support, please use the [official forum](https://forum.tagion.org/c/development/6) or [Telegram chat](https://t.me/tagionChat). The issue list of this repo is exclusively for bug reports and feature requests.

## Issues

Please use GitHub to [report a bug](https://github.com/tagion/alpha_one/issues/new?assignees=cbleser%2C+alexSushko&labels=bug&template=bug_report.md&title=) or [request a feature](https://github.com/tagion/alpha_one/issues/new?assignees=alexSushko%2C+cbleser&labels=enhancement&template=feature_request.md&title=).
