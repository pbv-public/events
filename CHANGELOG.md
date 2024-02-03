# Events Schema Changelog

## [v0.0.4](https://github.com/pbv-public/events/releases/tag/v0.0.4) on 2024-Feb-03
> * [Compare to Previous Version](https://github.com/pbv-public/events/compare/v0.0.3...v0.0.4?expand=1)
> * Version Checksums: Functional=aaa28444947648beb849a54c058e483f Full=200725eda7c26f2fa62a6f47559168dc

* rename `Frame` to `Moment` and update documentation accordingly
  * `Rally.frames` is now `Rally.moments`
* rename `Ball Area` to `Zone` and tweak its documentation
  * `Frame.ball.ball_area` is now `Moment.ball.zone`
  * This aligns with the property names `start_zone` and `end_zone` already used inside shot to hold values of this type.
* rename `ball.shot.ball` to `ball.shot.resulting_ball_movement`
* add `ball.contact`
  * Previously, it was possible to compute the following:
    * A shot occurred if ball.shot was set
    * Net contact occurred if ball.ball_area == "net"
    * Otherwise a bounce occurred
  * This was tedious and overly complicated. It also didn't generalize well to our future intent of also communicating when a shot has hit a player ("body bag") or enable us to distinguish between a "bounce" and a ball just flying through the air (if for some reason it was worth including such a ball).
  * `ball.contact` vastly simplifies things while also giving us a path to adding new body bags (or possibly other things, e.g., "pole") in the future. Please see `ball.contact` for a description of the values this enum can take.
* rename `shot.ball.angle` to `shot.ball.angles.yaw`
  * This more clearly describes the value it contains. The description and value of the field is unchanged (see its description for more detail about what yaw means).
  * add `shot.ball.angle.pitch` - this new field is complementary to `yaw`.
* Other documentation changes (non-functional):
  * Updated the schema viewer web app to better display documentation for:
    * Map types using JSON Schema's `patternProperties` capability now show the type name
      for the values in the map (previously it only did this for the keys in the map)
    * Documentation for the key you're currently looking at used to only show that key's
      description. Now it shows any constraints (e.g., enum) as well (same as we do in
      the list of properties)
  * The value which `kitchen_changes` maps to now has a descriptive name _Kitchen Change
    Type_. It is still an enum which still only allows the values `"arrived"` or
    `"departed"`. This descriptive name now shows up in the web-based docs explorer. It
    also now shows up as a type in the side navigation bar.
  * The side navigation bar now also shows the `Moment` type.

-------------------------------------
## [v0.0.3](https://github.com/pbv-public/events/releases/tag/v0.0.3) on 2024-Jan-29
> * [Compare to Previous Version](https://github.com/pbv-public/events/compare/v0.0.2...v0.0.3?expand=1)
> * Version Checksums: Functional=77b59553def7fac9297952baa597a39f Full=408eb964050b22fb77238f07f88493aa

* Generalized Bounce Area to Ball Area and use it in several similar places throughout the schema

-------------------------------------
## [v0.0.2](https://github.com/pbv-public/events/releases/tag/v0.0.2) on 2024-Jan-26
> * [Compare to Previous Version](https://github.com/pbv-public/events/compare/v0.0.1...v0.0.2?expand=1)
> * Version Checksums: Functional=e1bf186f3760fdb685e646242c862eaf Full=b1e423b867a17559806cd0a03c430812

update readme

 * simplify setup - just one command to install all deps & build schemas
 * document how to run tests
 * document where built schema explorer web apps are deployed and how

-------------------------------------
## [v0.0.1](https://github.com/pbv-public/events/releases/tag/v0.0.1) on 2024-Jan-25
> * [Compare to Previous Version](https://github.com/pbv-public/events/compare/v0.0.1^...v0.0.1?expand=1)
> * Version Checksums: Functional=729fabf307f7e8edd90af24ef0037c43 Full=3bdefad6cd9584d5fb7467fb6d57faa4

fix dev and release docs merging

