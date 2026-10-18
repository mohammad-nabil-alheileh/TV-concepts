1. Platform.isTV

    It tells you at runtime whether the app is running on a TV (Android TV or Apple TV in the react-native-tvos fork). It also has an Apple-specific sibling, Platform.isTVOS.

        import { Platform } from 'react-native';

        const cardStyle = {
        width: Platform.isTV ? 320 : 160,
        margin: Platform.isTV ? 24 : 8, // TVs are viewed from far away
        };

        // Skip touch-only UI on TV
        {!Platform.isTV && <PullToRefresh />}

2. useTVEventHandler

    A hook that listens to remote control events globally: arrows, select, play/pause, and so on. It does not tell you which element is focused, only which key was pressed.

        import { useTVEventHandler } from 'react-native';

        function Player() {
        useTVEventHandler((evt) => {
            // eventKeyAction: 0 = key down, 1 = key up
            if (evt.eventType === 'playPause' && evt.eventKeyAction === 0) {
            togglePlayback();
            }
            if (evt.eventType === 'right' && evt.eventKeyAction === 0) {
            seekForward(10);
            }
        });

        return <Video /* ... */ />;
        }


3. BackHandler

    Handles the Back button. Your handler returns true to say “I handled it” and block the default behavior, or false to let the next handler act.

        import { useEffect } from 'react';
        import { BackHandler } from 'react-native';

        function Screen({ onClose, isMenuOpen, closeMenu }) {
        useEffect(() => {
            const sub = BackHandler.addEventListener('hardwareBackPress', () => {
            if (isMenuOpen) {
                closeMenu();
                return true;   // consumed: don't leave the screen
            }
            return false;    // let navigation/system handle it
            });
            return () => sub.remove(); // always clean up
        }, [isMenuOpen]);
        }