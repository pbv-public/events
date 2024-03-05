# Events Schema Changelog

## [v0.0.6](https://github.com/pbv-public/events/releases/tag/v0.0.6) on 2024-Mar-05
> * [Compare to Previous Version](https://github.com/pbv-public/events/compare/v0.0.5...v0.0.6?expand=1)
> * Version Checksums: Functional=1d8357a0445c4f28b2a2c53c97b4d244 Full=036ceee0daec12aafc9f802437c75ac7

- renamed moments -> ball -> shot -> `type` to `trajectory_type`
- valid trajectory types are one of smash | lob | dink | drive | drop
- a `trajectory_type` is omitted if unknown

-------------------------------------
## [v0.0.5](https://github.com/pbv-public/events/releases/tag/v0.0.5) on 2024-Feb-15
> * [Compare to Previous Version](https://github.com/pbv-public/events/compare/v0.0.4...v0.0.5?expand=1)
> * Version Checksums: Functional=21967e5231867c9ce2e91905435a3ed6 Full=01233c3bdeb05cbddf127ca7d5df65cc

* `Moment.players` (type = `Player Snapshot`) now contains information about
  each player at a given moment including _both_ their position (previously in
  `Moment.player_positions`) and their kitchen change events (previously in
  `Moment.kitchen_changes`). The motivations for this change include:
  * Before, player position was required. But sometimes the player's position is not
    known and thus we should omit it. This should only happen in rare cases like if the
    player runs out of the video frame (e.g., to fetch a lost ball).
  * The Map being used to store kitchen_changes was a little awkward because its keys
    had to be strings (JSON object keys must be strings) but player IDs are ints. That
    awkwardness goes away now that we have an array of players.
  * If we add more per-moment player stats in the future, they'll naturally be added as
    additional keys in `Player Snapshot`.
* `Shot.ball.height_over_net` is now optional. It is omitted if the ball never _reaches_
   the net after being hit (e.g., it goes backwards or off to the side).
* `resulting_ball_movement.angles` has a revised definition for yaw and pitch which is
  more intuitive.
  * Pitch defines the angle the ball is going up or down.
  * Yaw defines the direction (forwards, backwards, to the side) the ball is going.
* Documentation only changes:
  * `height_over_net` and `crossed_net` documentation updated to explain that these
    fields refer to the net plane (i.e., the plane at `y=0.5`).
  * Fixed a bug in the schema viewer web app. It was showing the type's description even
    if the property had a custom description. For example, `shot.player_id`'s description
    should read "the player who hit the ball". Clicking on that property will take you to
    the documentation for the `Player ID` type (which documents how we number players.)

-------------------------------------
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

