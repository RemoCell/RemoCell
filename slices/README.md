# RemoCell GRID

Imagine this as a filesystem directory subtree for storage/indexing of uneven, and potentially
dense, geolocated data. It's based on latitude and longitude (in degrees as decimal numbers). Based
on data format from Android GPS API.

## STRUCTURE

(Directories exist only where data exists. So directories at any level are created only when needed.)

Exactly four levels of directories. Data files exist only at the bottom level, which we call "leaf
buckets".

1. "Latitude whole degree". As two digits (with a leading zero if needed, so 0-9th parallels are
   prefixed with `0`). Prefixed with
 - `P` for positive (North of the equator), and
 - `N` for negative (South of the equator).

2. "Latitude decimal digit" (first digit of the decimal fraction, `0-9`).

3. "Longitude whole degree". As three digits (with any leading zeros, so
   - 0-9th meridians areprefixed with `00`, and
   - 10-99th meridians are prefixed with `0`).
   Prefixed with
   - `P` for positive (East of Greenwich, UK), and
   - `N` for negative (West of Greenwich, UK).

4. "Longitude decimal digit" (first digit of the decimal fraction).

(Any exact zero coordinate is deemed to be positive. So any point exactly on the equator (0th
parallel) is deemed to have `P00` latitude, and any point on the standard 0th meridian (one crossing
Greenwich, England) is deemed to have `P000` longitude.)

## MAPPING TO FLAT LEVEL

RemoCell's large data (cell coverage)( is NOT stored in the above four-level uneven tree structure
in GIT (because of GitHub repository size limitations). Instead, it's in flat (one level) storage of
GitHub "releases".

For any coordinate, we can match its "leaf bucket" as a four-level directory path above. For each
such leaf bucket and for each carrier with data in the area there is exactly one GitHub "release"
file, with a name based on the four-level directory path.

For example, a release file for path `P47/0/N122/0` (in the north west USA) could be
`P47-0-N122-0`.

## SPLITTING and BALANCING

We have a threshold for size of leaf "releases" files under any leaf bucket. Once exceeded, we split
that leaf bucket. We cut it in half, but which way?

(We pretend that the world is flat.) Initially, a leaf bucket is a square (1 degree x 1 degree).
Over time, most bucket will be cut into rectangles (but they may become squares again).

We pretend that a content of the bucket is spread evenly (throughout its rectangle/square). Then an
optimal way to split such a bucket is to cut it parallel to its shorter side - like when you are
folding a sheet of paper into a half (for most purposes).

However, different direction of cutting has different costs:

- A "horizontal" cut is along a parallel. We split
  - a respective level `#2` "latitude decimal part" bucket. That means we also have to split all of
  its deeper buckets:
  - all level `#3` "longitude whole degree" buckets, their
  - level `#4` "longitude decimal part" buckets and their
  - level `#5` carrier buckets.
  
  That's `2 x N x P x Q` time complexity of re-organizing.
  
- A "vertical cut" is along a meridian. We split its
  -  level `#4` "longitude decimal part" bucket:  just one, and its
  -  level `#5` carrier buckets.

  That's `2 x Q` time complexity of re-organizing.

So, if it were possible, we'd always prefer vertical cuts. However, we need to cut horizontally, too
at least occasionally. Otherwise the data sizes would be "unbalanced". That would affect not only
server storage, but also user download bandwidth/time and local cell phone storage. 

Otherwise, you may want to download data for a small area, but it could come with a heavy load of
many neighboring thin vertical slices only because our chosen area fits into all of them. And, we
don't need most of the data of those thin slices!

But, if we "balance" the shape of the leaf buckets, that problem is unlikely. We may have big
downloads, but the content will be more relevant to us.

### SPLITTING: RULES OF THUMB

- If a leaf bucket is square, or a horizontal rectangle, we cut it vertically.
- If a leaf bucket is a vertical rectangle up to certain ratio, still cut it vertically.
- If a leaf bucket is 
