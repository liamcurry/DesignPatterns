+++
date = "2015-03-19T10:07:51-06:00"
draft = true
title = "The Strategy Pattern"

+++

## ELI5
Let's say you have a new race car track playset. The tracks come in little
pieces that you, or a best friend, or mommy or daddy, can put together in
many different ways. Let's say this is a **really cool** play set, and includes
a big red button that rockets the race car onto the track. The whole thing works
great, as long as you connect the track to the big red button.

You like big red buttons, so daddy makes three or four different race tracks.
You can then choose which one you want to race on next, and daddy plugs it in
to the big red button. All you have to do is press the button, and watch the
race cars zoom along the race track.

The *Strategy Pattern* can be seen here. An algorithm is declared (race cars
can be shot down a race track by pressing a big red button). The type of track,
the color of the cars, etc, can vary from track to track. Each works though, as
long as it connects to the big red button that fires them off.

## Code Samples

### Java
{{< highlight java >}}
public interface RaceTrack() {
  public void startRace();
}

public class RaceTrackA implements RaceTrack {
  public void startRace() {
    turnRight();
    turnRight();
    turnLeft();
  }
}

public class RaceTrackB implements RaceTrack {
  public void startRace() {
    doBarrelRoll();
    turnLeft();
    doLoop();
  }
}

public class BigRedButton() {
  public void pressButton() {
    List&lt;RaceTrack&gt; tracks = new ArrayList&lt;RaceTrack&gt;();
    tracks.add(new RaceTrackA());
    tracks.add(new RaceTrackB());

    for (RaceTrack track : tracks) {
      track.startRace();
    }
  }
}
{{< /highlight >}}

### Explanation

The code sample above illustrates the description at the beginning of this
page. An interface, `RaceTrack`, contains one method, `startRace()`. We can
then implement the interface any number of times, and flesh out that method.
We do this a few times (with `RaceTrackA` and `RaceTrackB`).

The Strategy Pattern's benefit shows itself within our iterator block, where we
traverse over a list of `RaceTrack` objects. For each `RaceTrack`, we invoke the
`startRace()` method. This method does different things, depending on the
implemention, but to our parent class, it's all the same.
