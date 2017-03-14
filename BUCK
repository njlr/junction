include_defs('//BUCKAROO_DEPS')

def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

JUNCTION_CONFIG_H = """
#define JUNCTION_WITH_FOLLY 0
#define JUNCTION_WITH_CDS 0
#define JUNCTION_WITH_NBDS 0
#define JUNCTION_WITH_TBB 0
#define JUNCTION_WITH_TERVEL 0
#define JUNCTION_WITH_LIBCUCKOO 0
#define NBDS_USE_TURF_HEAP 0
#define TBB_USE_TURF_HEAP 0
#define JUNCTION_TRACK_GRAMPA_STATS 0
#define JUNCTION_USE_STRIPING 1

#include \\"junction_userconfig.h\\"
"""

genrule(
  name = 'junction_config.h',
  out = 'junction_config.h',
  cmd = 'echo "' + JUNCTION_CONFIG_H + '" > $OUT',
)

genrule(
  name = 'junction_userconfig.h',
  out = 'junction_userconfig.h',
  cmd = 'touch $OUT',
)

cxx_library(
  name = 'junction',
  header_namespace = 'junction',
  exported_headers = merge_dicts(subdir_glob([
    ('junction', '**/*.h'),
  ]), {
    'junction_config.h': ':junction_config.h',
    'junction_userconfig.h': ':junction_userconfig.h',
  }),
  srcs = glob([
    'junction/**/*.cpp',
  ]),
  compiler_flags = [
    '-std=c++11',
  ],
  visibility = [
    'PUBLIC',
  ],
  deps = BUCKAROO_DEPS,
)
