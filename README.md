## Project Description

This is a Bazel project configured with **cifuzz** which includes:

- multiple packages
- two Fuzz Tests
  - `main/tests:explore_me_fuzz_test`, defined in the same package as the source
    code
  - `fuzztests:test_me_fuzz_test`, located in a separated package

## Run

### Heap Buffer Overflow and Undefined Behaviour

```
cifuzz run main/tests:explore_me_fuzz_test
```

### Heap Use After Free

```
cifuzz run fuzztests:test_me_fuzz_test
```

## Bundle

### explore_me_fuzz_test

```
cifuzz bundle main/tests:explore_me_fuzz_test
```

The bundle should include **1** Fuzz Test with **2** targets to cover fuzzing 
and coverage builds:

```
...
target: main/tests/explore_me_fuzz_test
path: libfuzzer/address+undefined/main/tests/explore_me_fuzz_test/bin/explore_me_fuzz_test
...
target: main/tests/explore_me_fuzz_test
path: replayer/coverage/main/tests/explore_me_fuzz_test/bin/explore_me_fuzz_test
```

### test_me_fuzz_test

```
cifuzz bundle
```

The bundle should include **1** Fuzz Test with **2** targets to cover fuzzing 
and coverage builds:

```
...
target: fuzztests/test_me_fuzz_test
path: libfuzzer/address+undefined/fuzztests/test_me_fuzz_test/bin/test_me_fuzz_test
...
target: fuzztests/test_me_fuzz_test
path: replayer/coverage/fuzztests/test_me_fuzz_test/bin/test_me_fuzz_test
...
```

## Coverage

### explore_me_fuzz_test

```
cifuzz coverage main/tests:explore_me_fuzz_test
```

```
                               File | Functions Hit/Found |  Lines Hit/Found | Branches Hit/Found
            main/src/explore_me.cpp |      1 / 1 (100.0%) | 15 / 15 (100.0%) |     8 / 8 (100.0%)
main/tests/explore_me_fuzz_test.cpp |      2 / 2 (100.0%) |   8 / 8 (100.0%) |     0 / 0 (100.0%)
                                    |                     |                  |
                                    | Functions Hit/Found |  Lines Hit/Found | Branches Hit/Found
                              Total |               3 / 3 |          23 / 23 |              8 / 8
```

### test_me_fuzz_test

```
cifuzz coverage fuzztests:test_me_fuzz_test
```

```
                           File | Functions Hit/Found | Lines Hit/Found | Branches Hit/Found
fuzztests/test_me_fuzz_test.cpp |      2 / 2 (100.0%) |  6 / 6 (100.0%) |     0 / 0 (100.0%)
                                |                     |                 |
                                | Functions Hit/Found | Lines Hit/Found | Branches Hit/Found
                          Total |               2 / 2 |           6 / 6 |              0 / 0
```
