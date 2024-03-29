# Copyright (c) PLUMgrid, Inc.
# Licensed under the Apache License, Version 2.0 (the "License")

find_program(ARPING arping)
if(ARPING STREQUAL "ARPING-NOTFOUND")
  message(WARNING "Recommended test program 'arping' not found")
endif()
find_program(NETPERF netperf)
if(NETPERF STREQUAL "NETPERF-NOTFOUND")
  message(WARNING "Recommended test program 'netperf' not found")
endif()
find_program(IPERF iperf)
if(IPERF STREQUAL "IPERF-NOTFOUND")
  find_program(IPERF3 iperf3)
  if(IPERF3 STREQUAL "IPERF3-NOTFOUND")
    message(WARNING "Recommended test program 'iperf' or 'iperf3' not found")
  endif()
endif()

add_test(NAME py_test_bpf_log WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_bpf_prog sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_bpf_log.py)
add_test(NAME py_test_stat1_c WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_stat1_c namespace ${CMAKE_CURRENT_SOURCE_DIR}/test_stat1.py test_stat1.c)
add_test(NAME py_test_xlate1_c WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_xlate1_c namespace ${CMAKE_CURRENT_SOURCE_DIR}/test_xlate1.py test_xlate1.c)
add_test(NAME py_test_call1 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_call1_c namespace ${CMAKE_CURRENT_SOURCE_DIR}/test_call1.py test_call1.c)
add_test(NAME py_test_trace2 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_trace2 sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_trace2.py)
add_test(NAME py_test_trace3_c WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_trace3_c sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_trace3.py test_trace3.c)
add_test(NAME py_test_trace4 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_trace4 sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_trace4.py)
add_test(NAME py_test_trace_maxactive WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_trace_maxactive sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_trace_maxactive.py)
add_test(NAME py_test_probe_count WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_probe_count sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_probe_count.py)
add_test(NAME py_test_debuginfo WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_debuginfo sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_debuginfo.py)
add_test(NAME py_test_brb WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_brb_c sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_brb.py test_brb.c)
add_test(NAME py_test_brb2 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_brb2_c sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_brb2.py test_brb2.c)
add_test(NAME py_test_clang WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_clang sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_clang.py)
add_test(NAME py_test_histogram WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_histogram sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_histogram.py)
add_test(NAME py_array WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_array sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_array.py)
add_test(NAME py_uprobes WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_uprobes sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_uprobes.py)
add_test(NAME py_uprobes_2 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_uprobes2 sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_uprobes2.py)
add_test(NAME py_test_stackid WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_stackid sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_stackid.py)
add_test(NAME py_test_tracepoint WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_tracepoint sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_tracepoint.py)
add_test(NAME py_test_perf_event WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_perf_event sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_perf_event.py)
add_test(NAME py_test_attach_perf_event WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_attach_perf_event sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_attach_perf_event.py)
add_test(NAME py_test_utils WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_utils sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_utils.py)
add_test(NAME py_test_percpu WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_percpu sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_percpu.py)
add_test(NAME py_test_dump_func WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_dump_func simple ${CMAKE_CURRENT_SOURCE_DIR}/test_dump_func.py)
add_test(NAME py_test_disassembler WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_disassembler sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_disassembler.py)
add_test(NAME py_test_tools_smoke WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_tools_smoke sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_tools_smoke.py)
add_test(NAME py_test_tools_memleak WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_tools_memleak sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_tools_memleak.py)
if(NOT(CMAKE_SYSTEM_PROCESSOR STREQUAL "ppc64le" OR CMAKE_SYSTEM_PROCESSOR STREQUAL "ppc64"))
	add_test(NAME py_test_usdt WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	  COMMAND ${TEST_WRAPPER} py_test_usdt sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_usdt.py)
	add_test(NAME py_test_usdt2 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	  COMMAND ${TEST_WRAPPER} py_test_usdt2 sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_usdt2.py)
	add_test(NAME py_test_usdt3 WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	  COMMAND ${TEST_WRAPPER} py_test_usdt3 sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_usdt3.py)
endif()
add_test(NAME py_test_license WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_license sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_license.py)
add_test(NAME py_test_free_bcc_memory WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_free_bcc_memory sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_free_bcc_memory.py)
add_test(NAME py_test_rlimit WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_rlimit sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_rlimit.py)
add_test(NAME py_test_lpm_trie WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_lpm_trie sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_lpm_trie.py)
add_test(NAME py_ringbuf WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_ringbuf sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_ringbuf.py)
add_test(NAME py_queuestack WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_queuestack sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_queuestack.py)
add_test(NAME py_test_map_batch_ops WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_map_batch_ops sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_map_batch_ops.py)
add_test(NAME py_test_map_in_map WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${TEST_WRAPPER} py_test_map_in_map sudo ${CMAKE_CURRENT_SOURCE_DIR}/test_map_in_map.py)
