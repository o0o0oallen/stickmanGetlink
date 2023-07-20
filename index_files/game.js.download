window.boot = function () {

    var settings = window._CCSettings;
    window._CCSettings = undefined;

    cc.assetManager.init({
        bundleVers: settings.bundleVers,
        subpackages: settings.subpackages,
        remoteBundles: settings.remoteBundles,
        server: settings.server,
        subContextRoot: settings.subContextRoot
    });

    function cb(err) {
        if (err) return console.error(err.message, err.stack);
        if (--rest <= 0) {
            cc.game.run({
                id: 'GameCanvas',
                debugMode: settings.debug ? cc.debug.DebugMode.INFO : cc.debug.DebugMode.ERROR,
                showFPS: settings.debug,
                frameRate: 60,
                groupList: settings.groupList,
                collisionMatrix: settings.collisionMatrix
            }, function () {

                cc.view.enableRetina(true);
                cc.view.resizeWithBrowserSize(true);

                cc.director.loadScene(settings.launchScene, null, function () {

                    //console.log('Success to load scene: ' + settings.launchScene);

                });

            });
        }
    }

    var bundleRoot = ["internal", "main"];
    var rest = bundleRoot.length + 1;
    for (var i = 0; i < bundleRoot.length; i++) {
        cc.assetManager.loadBundle(bundleRoot[i], cb);
    }

    var jsList = [
        "pako.min.js",
        "thinkingdata.mg.cocoscreator.min.js"
    ];
    var i = jsList.length;
    while (i--) {
        jsList[i] = window.webPath + "src/" + jsList[i];
    }
    cc.assetManager.loadScript(jsList, cb);

};
