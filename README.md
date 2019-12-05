# svelte-gravatar
Svelte component for rendering a gravatar profile image. Adjusts automatically to HiDPI displays.

Based on the brilliant [react-gravatar](https://github.com/KyleAMathews/react-gravatar/blob/master/README.md) from Kyle Mathews.

## Build status

[![CircleCI](https://circleci.com/gh/DPr00f/svelte-gravatar/tree/master.svg?style=svg)](https://circleci.com/gh/DPr00f/svelte-gravatar/tree/master)

## Demo

## Usage
See https://en.gravatar.com/site/implement/images/ for documentation on
all the options.

### Avoid exposing email
If you wish to avoid sending an email address to the client, you can
compute the md5 hash on the server and pass the hash to the component
using the `md5` prop instead of the `email` prop.

### Defaults
* 50x50 image
* g rated photos
* alt as `Gravatar for {email}`
* retro backup faces for emails without profiles
* only load image when on the screen

### Props

* size
* alt
* rating = 'g';
* md5
* protocol
* email
* useWaypoint
* waypointOptions - Please refer to [svelte-waypoint](https://github.com/matyunya/svelte-waypoint)
* domain
* default
* class
* style

### Use defaults
`<Gravatar email="jocolopes@gmail.com" />`

### Override all defaults

`<Gravatar
  email="jocolopes@gmail.com"
  size={100}
  rating="pg"
  default="monsterid"
  alt="Image from email"
  useWaypoint={false}
  domain="www.gravatar.com"
  protocol="http://"
/>`
