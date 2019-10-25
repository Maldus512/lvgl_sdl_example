import os
import multiprocessing

PROGRAM = "program"
LVGL = "lvgl"
CFLAGS = ["-Wall", "-Wextra", "-g", "-O0", "-DLV_CONF_INCLUDE_SIMPLE",
          "-DLV_CONF_INCLUDE_SIMPLE", "-DLV_LVGL_H_INCLUDE_SIMPLE"]
LDLIBS = ["-lSDL2"]

# Creates a Phony target


def PhonyTargets(
        target,
        action,
        depends,
        env=None,
):
    if not env:
        env = DefaultEnvironment()
    t = env.Alias(target, depends, action)
    env.AlwaysBuild(t)

num_cpu = multiprocessing.cpu_count()
SetOption('num_jobs', num_cpu)
print("Running with -j {}".format(GetOption('num_jobs')))

externalEnvironment = {}
if 'PATH' in os.environ.keys():
    externalEnvironment['PATH'] = os.environ['PATH']

env_options = {
    "ENV": externalEnvironment,
    "CPPPATH": ["{}/src".format(LVGL), LVGL, "src", "lv_drivers", "lv_examples/lv_apps", "."],
    "CCFLAGS": CFLAGS,
    "LIBS": LDLIBS,
}


sources = Glob("src/*.c")
sources += Glob("lv_drivers/display/monitor.c")
sources += Glob("lv_drivers/display/fbdev.c")
sources += Glob("lv_examples/lv_apps/demo/*.c")
sources += Glob("lv_drivers/indev/*.c")
sources += Glob("lvgl/src/*.c")
sources += Glob("lvgl/src/**/*.c")

env = Environment(**env_options)

p = env.Program(PROGRAM, sources)
