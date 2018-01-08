# ds_profiler
Simple profiler

## How to use it

### Include the header

```
#define DS_PROFILER
#include <ds_profiler.h>
```

### Initialize

```
perf::init();
```

### Use it

```
perf::reset();
while (running) {
    {
	    perf::ZoneTracker("Main");
        // your code
    }
}
perf::finalize();
```

### Performance output using ds_imgui

```
for (int i = 0; i < perf::num_events(); ++i) {
	const char* n = perf::get_name(i);
	float avg = perf::avg(i);
	if (n != 0 && avg > 0.0f) {
		gui::FormattedText("%-24s %2.6f", n, avg);
	}
}
```

### Shutdown

```
perf::shutdown();
```

