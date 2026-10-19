TV app targets several platforms with different capabilities. Tizen and webOS run a web runtime, while Android TV and Apple TV run native React Native. The same feature needs different code on each.

Instead of writing if (platform === 'tizen') inside feature code, you keep one file per platform with the same name, and the bundler picks the right one at build time.


How the file is chosen

    The bundler has an ordered list of extensions per build target. It tries them in order and uses the first file that exists.

        For a Tizen build, the list is:

            .tizen.web.tsx (most specific: Tizen only)
            .web.tsx (any web-runtime target)
            .tsx (generic fallback)



Metro (Android TV, Apple TV) has its own platform extensions (.android.tsx, .ios.tsx, .native.tsx).