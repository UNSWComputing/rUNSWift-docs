#########
CleverNao
#########

CleverNao is a machine learning system designed to optimise values with minimal training data. Currently this is only
used by the automatic kick lean calibration, but it is designed to be easily extended to other problems. CleverNao is
based on the `Gaussian Process`_ (GP), which is a computationally intensive but data efficient machine learning tool.

.. _Gaussian Process: https://www.researchgate.net/publication/41781206_Gaussian_Processes_in_Machine_Learning

****************
Gaussian Process
****************

Gaussian Process (GP) can be difficult to wrap your head around, and the extremely technical language often used to
describe them doesn't help. Here I'll try to give a simple, non mathematical explanation. A GP can be thought of like
Bayesian Reasoning for functions. In Bayesian reasoning you start with some prior belief about the world ("It's
probably not raining"). You then make an observation ("Jane says it's raining.") and update that belief ("It's
probably raining"). The mathematics of Bayesian reasoning can account for uncertainty in your observations (If Jane
lies frequently you might conclude there's a 50% chance it's raining).

A GP does this in a continuous space. Take the nao kick lean optimisation case. In this problem the nao wants to kick
the ball while remaining as stable as possible. To do this it must optimise how far to the side it leans during each
kick. The kick lean can be any value. For each of these values you can imagine the nao has some belief about how stable
the kick will be (the mean). It also has some idea of how confident it is about this belief (the variance).

The nao then kicks the ball with  some lean value it can observe how stable it is during the kick. If it's more stable
than expected, the nao adjusts its expected mean up. If it's less stable than expected, the nao adjusts its expected
mean down. Either way, the nao is more confident about its belief in how stable kicks with that lean value will be, so
it adjusts its variance down. Since we'd expect kick lean values close to the one we tried to have similar performance,
we can make similar adjustments to them, with smaller adjustments as we get farther away.

At any time one particular lean value will have the best estimated stability. This is the kick lean the nao currently
thinks is the best to use. However, other kick leans with lower mean values might have higher uncertainty (variance),
which means they may actually be better than the current kick lean. The kick lean with the highest mean and uncertainty
is the best experiment the nao can perform if it wants to keep looking for more stable kicks. This gives the nao a
learning cycle. Calculate the best experiment. Perform the experiment. Update the model. Calculate the next best
experiment, and so on.

This is how CleverNao optimises parameters. It takes some set of parameters you want to optimise, then requests an
experiment. It waits for the nao to perform that experiment, then takes a single value indicating the "quality" of the
experiment (i.e. how stable the kick was). It updates the GP with this new data, then selects another experiment.

**********
Situations
**********

CleverNao can optimise the same set of parameters for several related situations. When a nao kicks it need to shift its
foot farther out or closer in to account for exactly where the ball is relative to its foot. Since the nao is moving its
foot differently a different kick lean is optimal. For this reason the kick lean optimiser uses a "situation". The
situation is just where exactly the ball is horizontally, relative to the nao's foot. The nao performs the best
experiment for that situation. Since the situation is just another value in the GP, the model will account for the fact
that kicks in two similar situations with similar kick lean values will have similar stability.
