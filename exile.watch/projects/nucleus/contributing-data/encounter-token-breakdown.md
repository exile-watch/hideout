# Encounter token breakdown

## API

<table><thead><tr><th width="169" align="center">key</th><th width="106" align="center">necessity</th><th width="105" align="center">type</th><th>description</th><th>Example</th></tr></thead><tbody><tr><td align="center">map</td><td align="center">optional</td><td align="center">string</td><td>Map name. In case there is no map for the boss (see: <code>conquerors</code> or <code>elder guardians</code>) then this field is ommited</td><td>Coves</td></tr><tr><td align="center">bosses</td><td align="center">required</td><td align="center">string</td><td><p>Boss name. </p><p>Can be multiple</p></td><td>Telvar, the Inebriated</td></tr><tr><td align="center">type</td><td align="center">optional</td><td align="center">string[]</td><td>List of ability damage types.</td><td>physical, fire</td></tr><tr><td align="center">abilities</td><td align="center">required</td><td align="center">string[]</td><td>List of <code>boss abilities</code></td><td>Spawn Barrel, Tar</td></tr><tr><td align="center">tip</td><td align="center">required</td><td align="center">string[]</td><td>List of Player Interactions to given Ability. <code>yml</code> brackets have the same role as dashes.</td><td>dodge, kill new spawns</td></tr><tr><td align="center">gif</td><td align="center">required</td><td align="center">string</td><td>Video source. Currently all of the sources are hosted from <code>http://gyazo.com/</code></td><td><a href="https://i.gyazo.com/279f86d6f8652e9708cde4a80276223c.mp4">https://i.gyazo.com/279f86d6f8652e9708cde4a80276223c.mp4</a></td></tr><tr><td align="center">about</td><td align="center">required</td><td align="center">string[]</td><td>About ability list. Wrap each sentence with double quotation marks (<code>""</code>). In future we may enhance those strings.</td><td>Every couple seconds Telvar throws Barrel at player's position</td></tr><tr><td align="center">isChallenge</td><td align="center">optional</td><td align="center">boolean</td><td>Marks ability as League Challenge</td><td>true, false</td></tr><tr><td align="center">aboutChallenge</td><td align="center">optional</td><td align="center">string[]</td><td>About League Challenge</td><td>Defeat Lycius, Midnight's Howl in Lair Map while he is channeling Wolf Barrage</td></tr></tbody></table>

## YAML example&#x20;

```yaml
map: Coves
bosses:
  - Telvar, the Inebriated:
      abilities:
        - Spawn Barrel:
            tip: [ destroy ]
            gif: https://i.gyazo.com/20b4ddbade91f264d18ba8c304d9a19a.mp4
            about:
              - "Every couple seconds Telvar spawns a Barrel at random position"
              - "Once destroyed leaves a pool of Tar"
        - Tar:
            tip: [ move out ]
            gif: https://i.gyazo.com/22602b30cc9cf622a91f1a0c371477d6.mp4
            about:
              - "Being in Tar slows your movement"
        - Throw Barrel:
            type: [ physical ]
            tip: [ dodge ]
            gif: https://i.gyazo.com/279f86d6f8652e9708cde4a80276223c.mp4
            about:
              - "Every couple seconds Telvar throws Barrel at player's position"
        - Alchemy Orb:
            type: [ fire ]
            gif: https://i.gyazo.com/22602b30cc9cf622a91f1a0c371477d6.mp4
            about:
              - "Alchemy Orb leaves a pool of flames"

  - Pirate Treasure:
      abilities:
        - Slam:
            type: [ physical ]
            tip: [ destroy ]
            gif: https://i.gyazo.com/20b4ddbade91f264d18ba8c304d9a19a.mp4
            about:
              - "Performs a deadly slam"
              - "This ability can explode Telvar's Barrel"
        - Whirling Blades:
            tip: [ dodge ]
            gif: https://i.gyazo.com/de274bac97aeea2ad5e7726b7c1250ab.mp4
            about:
              - "Rolls towards player linearly"
              - "This ability can explode Telvar's Barrel"
```

## Common tokens

In common cases you may notice we don't use "normal" strings but `tokens`. Pay attention to `about` key in example below:

```yaml
# coves.yml
map: Coves
bosses:
  - Telvar, the Inebriated:
      abilities:
        - Spawn Barrel:
            tip: [ destroy ]
            gif: https://i.gyazo.com/20b4ddbade91f264d18ba8c304d9a19a.mp4
            about:
              - /SPAWN_BARREL/
              - "Once destroyed leaves a pool of Tar"
```

In example above `/SPAWN_BARREL/` is a skill token which value is located in [tokens/skills.yml](https://github.com/sbsrnt/poe-watch/tree/main/tokens/skills.yml)

Skill token has 3 rules:

1. Must start with forward slash (`/`)
2. Must be upper-cased with underline in case ability name has more than 2 words
3. Must end with forward slash (`/`)

_example: `/SPAWN_BARREL/`, `/FIREBALL/`_

Since **standard** `yaml` files by definition are independent of each other we can't import in any shape or form values form other `yaml` file values nor make a use of [yaml anchors/aliases](https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/).

To make our lives easier and not duplicate definitions of common skills, in [scripts/encounters/extract-tokens.js](https://github.com/sbsrnt/poe-watch/tree/main/scripts/encounters/extract-tokens.js#L26-L36) we are replacing token(s) value for our [`.json` auto-generated](https://github.com/sbsrnt/poe-watch/tree/main/extracted-data/encounters) files.
