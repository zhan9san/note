# Snyk test

There are only 3 medium severity vulnerability found in ubuntu:latst image. This is a good example image to test.

```bash
--severity-threshold: low, medium and high
--fail-on: all, upgradable and patchable.
```

Based on the output of the test shell script, here is the conclusions

1. Once '--fail-on' is passed to snyk cli, no matter which level vulnerability is found, only if they are not upgradable or patchable, the test will pass.
2. If '--fail-on' is not passed to snyk cli, only if the vulnerability is lower than the level passed, the test will pass.
    1. If threshold=low or meduim, ubuntu test will not pass.
    2. If threshold=high, ubuntu test will not pass.

`test_snyk.sh`

```bash
#!/bin/bash
 
for threshold in "low" "medium" "high"
do
  for fail_on in "without_fail_on_option" "all" "upgradable" "patchable"
    do
      echo "threshold: " $threshold "fail_on: "$fail_on
      if [ $fail_on != "without_fail_on_option" ]
      then
        snyk container test --severity-threshold=$threshold --fail-on=$fail_on ubuntu > /dev/null 2>&1; echo $?
      else
        snyk container test --severity-threshold=$threshold ubuntu > /dev/null 2>&1; echo $?
      fi
  done
done
```

```bash
$ sh snyk_test.sh
Output:
 
threshold:  low fail_on: without_fail_on_option
1
threshold:  low fail_on: all
0
threshold:  low fail_on: upgradable
0
threshold:  low fail_on: patchable
0
threshold:  medium fail_on: without_fail_on_option
1
threshold:  medium fail_on: all
0
threshold:  medium fail_on: upgradable
0
threshold:  medium fail_on: patchable
0
threshold:  high fail_on: without_fail_on_option
0
threshold:  high fail_on: all
0
threshold:  high fail_on: upgradable
0
threshold:  high fail_on: patchable
0
```

## Reference

[Advanced failing of your builds with Snyk CLI](https://support.snyk.io/hc/en-us/articles/360019979978-Advanced-failing-of-your-builds-with-Snyk-CLI)
