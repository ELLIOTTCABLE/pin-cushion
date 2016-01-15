`pin-cushion` <img alt='Maintenance status: Maintained!' src="https://img.shields.io/badge/maintained%3F-yes-brightgreen.svg"><img src="http://elliottcable.s3.amazonaws.com/p/8x8.png"><a target="_blank" href="https://github.com/ELLIOTTCABLE/pin-cushion/releases"><img alt='Versions & releases' src="https://img.shields.io/npm/v/pin-cushion.svg"></a><img src="http://elliottcable.s3.amazonaws.com/p/8x8.png"><a target="_blank" href="https://npmjs.com/package/pin-cushion"><img alt='pin-cushion on the NPM registry' src="https://img.shields.io/npm/dt/pin-cushion.svg"></a><img src="http://elliottcable.s3.amazonaws.com/p/8x8.png"><a target="_blank" href="COPYING.text"><img alt='Open-source licensing details' src="https://img.shields.io/badge/license-ISC-blue.svg"></a><img src="http://elliottcable.s3.amazonaws.com/p/8x8.png"><a target="_blank" href="http://ell.io/IRC"><img alt='Chat on Freenode' src="https://img.shields.io/badge/chat-IRC-blue.svg"></a><img src="http://elliottcable.s3.amazonaws.com/p/8x8.png"><a target="_blank" href="http://twitter.com/ELLIOTTCABLE"><img alt='Twitter followers' src="https://img.shields.io/twitter/follow/ELLIOTTCABLE.svg?style=flat&label=followers&color=blue"></a>
=============
A simple command-line [Pinboard.in][] client:

    pin-cushion [verb] [arguments]
    pin-cushion posts/recent
    pin-cushion posts/suggest --url "http://www.ponylang.org"

    pb-rename() {
       pin-cushion tags/rename --old "$1" --new "$2"
    }

You get the idea. To use it, you must first record [your authentication token][auth] for the API:

    npm install -g pin-cushion
    pin-cushion --auth elliottcable:DEADBEEF1234567890

This only provides abstracted access to the Pinboard API as defined on their site:
#### <https://Pinboard.in/api>

Any Pinboard API method described there may be passed as the `verb`; and all described arguments are
accepted as command-line `flags`. These are not stored in this library; as your command-line
instructions are simply converted directly to API calls; so this tool probably doesn't need much in
the form of maintenance. `:P`

   [Pinboard.in]: <https://Pinboard.in/
   [auth]: <https://Pinboard.in/settings/password>

### Piping and JSON output
If not explicitly passed a `--format` parameter, then `pin-cushion` will spit out a formatted
object-description of the response, intended for human consumption. If a format is explicitly
provided, then the response from the server will be printed, unmodified; this is particularly useful
with the [`jq`](https://stedolan.github.io/jq/) command-line JSON manipulation tool:

    pin-cushion posts/recent --format=json | jq                      # Simply pretty-print
    pin-cushion posts/recent --format=json | jq '.posts[] | .href'   # Extract URLs of recent pins

This obviously lends itself to constructing complex shell pipes. Personally, I suggest aliasing
this:

    pc() { pin-cusion "$1" --format=json "$@" ;}
