# LanePrediction
The assumptions made for this methodology was that a driver tends to keep the vehicle in the same lane and changes lane
occasionally. 

Hence, in an ideal scenario, the perpendicular distance of the vehicle with respect to our road geometry remains
constant.



Such a scenario builds a hypothesis that presence of vehicle GPS location will peak at the centre
of the lane and reduce at the edges, representing a Gaussian distribution.
Hence, the perpendicular distance of vehicle trace from the reference line should follow a Gaussian
distribution, which peaks at the centre of the lane. Thereby, a Gaussian mixture clustering on the
vehicle data should provide us with the number of lanes in each direction.

However, this hypothesis turned out to be false because the captured vehicle GPS data is prone to error and most of the traces
were overlapping.

Hence, I developed a proprietary clustering technique to segregate the lanes in each direction. Below are the steps –
1. For each road geometry in each direction, only vehicles which had at least 2 traces were considered and its perpendicular
distance (in meters) from the reference line obtained.
2. In order to account for inaccuracies in capturing the GPS data a variance of 2 meters was considered acceptable in the
perpendicular distances (Logic - Width of a US lane is 3.7 meters, of which 50% is circa. 2 meters)
3. The mean of perpendicular distance was obtained for each vehicle and clusters were defined based on the width of a
lane in the US (3.7m)
4. 8 clusters were pre-defined, each with a width of 3.7 m and a cluster was predicted to be a lane only if at least 2 cars falls
in the same cluster. An additional cluster was labelled as ‘inlane’ if the reference line was part of a lane and cluster had
a width of 1.85 (=3.7/2)

Evaluation of the model is the most challenging part as; an unsupervised technique has been used for prediction. I decided to
carry out number of complementary evaluations using the other clustering approaches like agglomerative hierarchical
clustering, K means and also testing for Gaussian distribution within the data by performing Shapiro-Wilk Test and
D’Agostino’s K^2 Test
