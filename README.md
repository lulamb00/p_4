# API Design for Project 4

##Cache.c
###Buffer Cache
Purpose of Buffer Cache is to cache the data that is read or written in the disk

###Structure
The structure for the cache itself will be implemented as a list

Each entry of the cache will hold data
struct cache_entry
{
  uint8_t data[size of sector];
  
  disk_sector_t sector;
  
  bool accessed;
  
  bool dirty;
  
  struct list_elem elem;
}

###Eviction Policy
Let's first implement eviction with FIFO, when we are stuck with other tests or performance issues, use timer.

###Functions to implement

####cache_init()
Initialize the cache list

####cache_get_from_disk()
Get data from disk and make it into cache_entry, insert it in to cache. Evict if necessary

####cache_evict()
When the cache is full, Evict an entry to make space. When the entry it dirty, write to disk

####cache_write_to_disk()
Write the entry's data into corresponding disk sector

####cache_write_behind()
Checks the cache for dirty entry, When dirty entry is found, write to disk.
This function is called periodically, or when the system is halted.

####cache_read_ahead(disk_sector_t sector)
When trying to read from a disk sector, and when it is a cold read, read the furthur disk sector and insert it into the cache



