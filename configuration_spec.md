# Cron Timing Configuration

Options for specifying increments of execution. Because this is blockchain, there are new dimensions for specifying time increments.

### Consensus Based

Block, Epoch -- consensus based configurations execute at time of validation/propogation through a decentralized network.

### Timestamp Based

UTC, GMT -- timestamp based relies on earth clock time standards, where configurations are increments of base time units: seconds. More granular timing cannot be guaranteed since execution time is based on network consensus and propogation timing.


## Configuration

### Consensus

| Character | Description |
| ------- | ------- |
| * | any value |
| , | value list separator |
| - | range of values |
| / | step values |
| @epoch | alias to every "epoch" |

#### Examples

```
*/2 * (every even block for every epoch)
20 * (every 20th block after every epoch)
12000000 * (Only at block 12 million)
* 45000 (Only at epoch 45 thousand)
```

### Time Examples 

| Character | Description |
| ------- | ------- |
| * | any value |
| , | value list separator |
| - | range of values |
| / | step values |
| @yearly | (non-standard) |
| @monthly | (non-standard) |
| @weekly | (non-standard) |
| @daily | (non-standard) |
| @hourly | (non-standard) |

#### Examples

```
* * * * * (Every minute of every hour of every day of every month)
5 4 * * * (At 4:05, every day)
5 0 * 8 * (At 00:05, every August)
*/15 9-17 * * * (Every 15th minute during hours 9AM - 5PM)
0 0,12 1 */2 * (Every first minute past hour 0 and 12 on the 1st day of every 2nd month)
```
