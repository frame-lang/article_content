#PacManGhost

	-interface-

	start @(|>>|)
	stop @(|<<|)
	update
	
    -machine-

    $GameStart => $Default
		|>>|
			init()
			startUpdateTimer()
			-> $WanderAroundBase ^

    $WanderAroundBase => $Default
        |update|
            isPastSpawnTime() ?
                isPowerPelletActive()   ? -> $FleeFromPlayer ^ ::
                isPlayerDistanceClose() ?
                    -> $SeekTowardsPlayer ^
                :
                    -> $WanderAroundMaze ^
                ::
            :: ^

    $WanderAroundMaze => $Default
            |update|
                isPowerPelletActive()   ? -> $FleeFromPlayer ^ ::
                isPlayerDistanceClose() ? -> $SeekTowardsPlayer ^ ::
                ^

    $SeekTowardsPlayer => $Default
        |update|
            isPowerPelletActive()  ? -> $FleeFromPlayer ^ ::
            isPlayerDistanceClose() ? -> $WanderAroundMaze ^ ::
            ^

    $FleeFromPlayer => $Default
        |update|
            isEaten() ? -> $ReturnToBase() ^ ::
            isPowerPelletActive() ?!
                isPlayerDistanceClose() ?
                    -> $SeekTowardsPlayer ^
                :
                    -> $WanderAroundMaze ^
                ::
            :: ^

    $ReturnToBase => $Default
        |>| headToBase() ^
        |update|
            atBase() ?
                clearTimerAndEatenFlag() -> $WanderAroundBase
            :: ^

	$End
		|>| stopUpdateTimer() ^

    $Default
        |<<| -> $End ^

##
