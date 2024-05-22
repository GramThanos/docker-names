# Docker-Names

Docker Names generates semi-random, easy to remember names similar to how docker names its containers. For example, `desperate_fermi`, `cranky_heyrovsky` or `tender_mahavira`.

Or as seen from the docker client container list: 
![Docker container list](http://i.imgur.com/Ws7B38h.png)


Current Build Status: [![bearjaws](https://circleci.com/gh/bearjaws/docker-names.svg?style=svg)](https://github.com/bearjaws/docker-names)

### Usage

Usage is very simple as this module only exports one method:
```javascript
const dockerNames = require('docker-names');
console.log(dockerNames.getRandomName());
$ angry_nobel
```

Additionally, per dockers specification they have a "retry" counter that appends a *random** number if set to true or a number greater than 0.
For example:
```javascript
console.log(dockerNames.getRandomName(true));
$ jolly_mclean3

console.log(dockerNames.getRandomName(3));
$ backstabbing_roentgen5
```
`*` This uses Math.random which means its not very random. These names should never be used as any sort of unique id. The names are mostly applicable for small lists of ephemeral objects that you want to have easy to remember identifiers for.

Seeds** can be used to generate the same name for the same seed:
```javascript
const dockerNames = require('docker-names');
console.log(dockerNames.getRandomName(false, 'my-seed-here')); // Will always return the same name if the seed 'my-seed-here' is given
$ brave_ride
```
`**`(Antti Sykäri's algorithm is used for seedable pseudo random number generator)

You can pass your own custom random number generator, by supplying an object with a method `random` method (that returns values greater than or equal to 0 and less than 1):
```javascript
const dockerNames = require('docker-names');
console.log(dockerNames.getRandomName(false, {random : () => ((Math.random() + Math.random()) / 2)})); // Example of a custom random number generator
console.log(dockerNames.getRandomName(false, {random : () => 0.213456})); // Example of a not so random number generator (that will return determined_curie)

// Or set it globally for all names generations
dockerNames.random_number_generator = {random : () => ((Math.random() + Math.random()) / 2)};
console.log(dockerNames.getRandomName());
console.log(dockerNames.getRandomName());
```

### Word Lists

This module exports the full docker name lists as two arrays.
```javascript
// This contains all adjectives i.e. "left words"
dockerNames.adjectives = Array('admiring', 'adoring'...);

// This contains all surnames to use as "right words"
dockerNames.surnames = Array('albattani', 'allen' ...);
```
