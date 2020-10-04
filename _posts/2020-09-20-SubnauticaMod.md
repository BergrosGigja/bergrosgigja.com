---
title:        "Subnautica BZ Mod"
description:  "Making a mod for Subnautica Below Zero"
---

I have always been curious about how game mods are made but never taken the step to make one myself.

After playing Subnautica 2 for a while however, I started to think about some things I'd like to change and ended up making a [small mod](https://github.com/BergrosGigja/Subnautica-mod).
Subnautica made sense since it's made with Unity, so I knew I would'nt have an issue with the language or engine.

Without any previous knowledge I started to search and found sem very interesting information.

### Useful information

After reading a [tutorial](https://bitbucket.org/glibfire/subnauticamods/src/master/ModdingTutorial/ModdingTutorial.md) that covered the essentials I decided to get going.

These are all the tools needed:

- **Visual studio**
- **Unity 2019.x**
- **dbSpy**
- **QModManager**
- **SML Helper** (optional, specific version for BZ)

Additional information that helped a lot:
- [Patching Harmony](https://harmony.pardeike.net/articles/patching.html)
- [SML Helper wiki](https://github.com/SubnauticaModding/SMLHelper/wiki)
- [Harmony wiki](https://github.com/pardeike/Harmony/wiki)

### Setting up

After setting up a new project I added all the references needed.

```
SubnauticaZero/SubnauticaZero_Data/Managed/Assembly-CSharp.dll
SubnauticaZero/BepEx/core/0Harmony.dll
SubnauticaZero/BepEx/plugins/QModManager/QModInstaller.dll
SubnauticaZero/QMods/SMLHelper_BZ/SMLHelper.dll

SubnauticaZero/SubnauticaZero_Data/Managed/UnityEngine.dll
and UnityEngine.CoreModule (for monobehavior scrips)
```

I needed to start with something simple yet useful.
There is one thing I don't particularly care for in Subnautica BZ, that is the iceworm attacks.
I think anyone that has played the game would understand why it would be nice to disable the attacks completely.
Disabling it would allow me to explore in peace.

After a few tries I managed to find the method triggering the worm.

```
[QModCore]
    public static class Main
    {
        [QModPatch]
        public static void Patch()
        {
            Harmony.CreateAndPatchAll(Assembly.GetExecutingAssembly(), "com.disablewormattack.psmod");
        }
    }

    [HarmonyPatch(typeof(IceWormHuntModeTrigger), nameof(IceWormHuntModeTrigger.OnPlayerEnter))]
    internal static class IceWormHuntModeTrigger_Override
    {
        [HarmonyPrefix]
        internal static bool Prefix()
        {
            return false;
        }
    }

```

Next I thought it would be good to set up some options to the option menu at start.
I managed to add an option to disable the attacks which saves your preference.

Now my small mod is ready, pretty cool.

For anyone interested, the [offical discord](https://discord.gg/VAnD3mS) also has a lot of information, help to set up mods and make mods.
They also have mod ideas and a place for people to find others to collaborate with.

