![hitobito logo](https://hitobito.com/images/logo.svg)

#
# Welcome to hitobito 人人

hitobito is an open source web application to manage organisation and communities with complex group hierarchies with members, events, courses, mailings, communication and a lot more.

[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/hitobito/hitobito/graphs/commit-activity) 
[![Documentation Status](https://readthedocs.org/projects/hitobito/badge/?version=latest)](https://hitobito.readthedocs.io/?badge=latest)
[![GitHub](https://img.shields.io/github/license/hitobito/hitobito)](https://github.com/hitobito/hitobito/blob/master/LICENSE)
[![Open Source Helpers](https://www.codetriage.com/hitobito/hitobito/badges/users.svg)](https://www.codetriage.com/hitobito/hitobito)
[![Build Status](https://travis-ci.org/hitobito/hitobito.svg?branch=master)](https://travis-ci.org/hitobito/hitobito)

## Development

Check out our [development kit](https://github.com/hitobito/development/)

More detailed development documentation can be found in [doc/development](doc/development).

This is where you also find some [Deployment Instructions](doc/development/02_deployment.md).

## Architecture

The architecture documentation in German can be found in [doc/architecture](doc/architecture).

Two topics shall be mentioned here explicitly:

### Group Hierarchy

hitobito provides a powerful meta-model to describe group structures.
Groups are always of a specific type and are arranged in a tree.
Each group type may have several different role types.

This core part of hitobito does not provide any specific group or role types.
They have to be defined in a separate plugin, specific to your organization structure.

An example group type definition might look like this:

    class Group::Layer < Group
      self.layer = true

      children Group::Layer, Group::Board, Group::Basic

      class Role < Leader
        self.permissions = [:layer_full, :contact_data]
      end


      class Member < Role
        self.permissions = [:group_read]
      end

      roles Leader, Member
    end

A group type always inherits from the class `Group`.
It may be a layer, which defines a set of groups that are in a common permission range.
All subgroups of a layer group belong to this range unless a subgroup is a layer itself.

Then all possible child types of the group are listed.
When creating subgroups, only these types will be allowed.
As shown, types may be organized recursively.

For the ease of maintainability, role types may be defined directly in the group type.
Each role type has a set of permissions.
They are general indications of what and where.
All specific abilities of a user are derived from the role permissions she has in her different groups.

See [Gruppen- und Rollentypen](doc/architecture/08_konzepte.md) for more details and
[hitobito_generic](https://github.com/hitobito/hitobito_generic) for a complete example group
structure.


### Plugin architecture

hitobito is built on the plugin framework [Wagons](http://github.com/codez/wagons).
With Wagons, arbitrary features and extensions may be created for hitobito.
As mentioned above, as there are no group types coming from hitobito itself,
at least one wagon is required to define group types in order to use hitobito.

See [Wagon Guidelines](doc/development/04_wagons.md) or [Wagons](http://github.com/codez/wagons)
for more information on wagons and its available rake tasks.


## Community
hitobito made with 💙 and the incredible community:

* Jungwacht Blauring Schweiz
* [Puzzle ITC GmbH](https://www.puzzle.ch)
* Pfadibewegung Schweiz
* hitobito AG
* CEVI Regionalverband ZH-SH-GL / CEVI Schweiz
* Dachverband Schweizer Jugendparlamente DSJ
* Insieme Schweiz 
* Forschungstelle Digitale Nachhaltigkeit
* CH Open
* Schweizer Blasmusikverband
* CVP Schweiz
* Stiftung für junge Auslandschweizer

Please contact [KunoKunz](https://github.com/KunoKunz) if you want to be part of our community.

## License

hitobito is released under the [GNU Affero General Public License](LICENSE).

The hitobito logo is a registered trademark of hitobito LTD, Switzerland. 

---

btw: hitobito 人人 [means](https://www.wordsense.eu/%E4%BA%BA%E4%BA%BA/) "everyone"  
