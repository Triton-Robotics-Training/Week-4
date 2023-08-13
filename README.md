a

# Motors

There are about three types of CAN Motors we use:

They program slightly differently, which is why it’s necessary for the code to
know which motor on which port is which type.

| GM6020                 | M3508                                     | M2006                                     |
| ---------------------- | ----------------------------------------- | ----------------------------------------- |
| ![](assets/gm6020.png) | <img src="assets/m3508.png"  width="200"> | <img src="assets/m2006.png"  width="100"> |

| True ID | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| M3508   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | DNE | DNE | DNE | DNE |
| M2006   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | DNE | DNE | DNE | DNE |
| GM6020  | DNE | DNE | DNE | DNE | 1   | 2   | 3   | 4   | 5   | 6   | 7   | DNE |
