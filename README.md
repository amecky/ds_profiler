# ds_profiler

Very simple profiler used in my games. It is a single header C++ file. All you need is actually the ds_profiler.h file.

## How to use it

### Include the header

In *one* file you need to include the header and define DS_PROFILER to create the implementaton:

```
#define DS_PROFILER
#include <ds_profiler.h>
```

### Initialize

The profiler needs to be initialized before you can use it:

```
perf::init();
```

### Use it

Inside your main loop you need to call reset first and finalize at the end. Then use perf::ZoneTracker to measure the code.

```
while (running) {
    perf::reset();
    perf::ZoneTracker("Main");
    {
	    perf::ZoneTracker("Sub-Main");
        // your code
    }
    {
	    perf::ZoneTracker("More-Sub-Main");
        // your code
    }
    perf::finalize();
}
```

### Performance output using ds_imgui

This is an example about how to output the average time using ds_imgui:

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

At the end of your application call shutdown to clean up the profiler:

```
perf::shutdown();
```

