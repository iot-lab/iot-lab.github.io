---
title: UWB nodes position change In Toulouse
---

Following the installation of 46 new nodes, more work is coming in Toulouse :

- Some nodes will be slightly moved.
- A new ground truth will be measured and published

Several dwm1001 nodes were initially fixed to furniture which, with time, has created contradictory needs in an active office building :

- These furniture items should not be moved to maintain testbed reproducibility and an accurate ground truth
- It is sometimes required to move them (change in the floorplan, need to reach a socket behind a cabinet, ...)

To solve this, they will be mounted on the ceiling. We will attempt to put them as close as possible to their previous position but the mounting points cannot be installed arbitrarily, therefore there will be some change in their position on the XY plane (at most 35 cm). We will however set them at the same height. 

The following dwm1001 nodes will be impacted : 1, 2, 5, 6, 9, 10, 62, 69, 70, 77, 81, 85, 89, 93, 94.
These changes will occur over the coming weeks, starting today with nodes 69 and 70.

Because these dwm1001 nodes will move and we have recently installed new dwm3001 nodes, we will re-measure the ground truth. Since we now have access to a 3D LIDAR scanner, this new ground truth will have a 1mm accuracy over the whole building. The old node positions will be removed on the iot-lab website and on the MQTT broker as soon as the nodes are moved, and they will be updated as soon as the new ground truth is available.
