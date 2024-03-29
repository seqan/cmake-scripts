# SPDX-FileCopyrightText: 2006-2024 Knut Reinert & Freie Universität Berlin
# SPDX-FileCopyrightText: 2016-2024 Knut Reinert & MPI für molekulare Genetik
# SPDX-License-Identifier: BSD-3-Clause

cmake_minimum_required (VERSION 3.21)

include (FindPackageMessage)

# Uses `ccache` to cache build results.
#
# See also
# * https://ccache.dev/
# * https://cmake.org/cmake/help/latest/variable/CMAKE_LANG_COMPILER_LAUNCHER.html
option (USE_CCACHE "Use ccache if available." ON)

if (USE_CCACHE)
    find_program (CCACHE_PROGRAM ccache)

    if (NOT CCACHE_PROGRAM)
        find_package_message (CCACHE_PROGRAM "Ccache program:             not available" "[${CCACHE_PROGRAM}]")
    else ()
        find_package_message (CCACHE_PROGRAM "Ccache program:             available" "[${CCACHE_PROGRAM}]")

        set (CMAKE_CXX_COMPILER_LAUNCHER "${CCACHE_PROGRAM}" CACHE INTERNAL "")
        set (CMAKE_C_COMPILER_LAUNCHER "${CCACHE_PROGRAM}" CACHE INTERNAL "")

        set (CMAKE_CXX_LINKER_LAUNCHER "${CCACHE_PROGRAM}" CACHE INTERNAL "")
        set (CMAKE_C_LINKER_LAUNCHER "${CCACHE_PROGRAM}" CACHE INTERNAL "")
    endif ()
endif ()
