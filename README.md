This is a sample load test project, demonstrating jmeter and maven integration.
Please don't execute it with more than 1 thread as it uses publicly available application

You can set up a CI build based on this project and parameterize build as -

![Parameterized CI build](http://www.awesomescreenshot.com/upload/18268/18496/ca7668b5-b02b-4574-6602-3154ae947aec.png)

And now you can provide these values from building the job - 

![Execute CI Build](http://www.awesomescreenshot.com/upload/18268/18496/97c57696-fc89-479e-6f47-d518fce80b49.png)


To execute test locally execute following command - 

```
mvn DAPP_URL=newtours.demoaut.com -DUSERS=$USERS -DDURATION=$DURATION -DRAMPUP_PERIOD=$RAMPUP_PERIOD -DSTARTUP_DELAY=$STARTUP_DELAY clean verify
```
    
Replace $USERS with number of users you want to run test with. Specify required values for other parameters and execute the tests

Once test execution is over then you can browse through test results under - 

```
/target/jmeter/results/index.html directory
 ```
You can read more about maven [JMeter plugin](https://github.com/jmeter-maven-plugin/jmeter-maven-plugin)

~~Notice that if you want to mark CI build as fail on the basis of test results then you should use [JMeter Analysis Plugin] (https://github.com/afranken/jmeter-analysis-maven-plugin) and set the threshold level~~

Don't use JMeter Analysis Plugin as it requires result files to be in xml format which is more resource comsuming than csv file. Set following property to generate results in csv format - ```<resultsFileFormat>csv</resultsFileFormat>```

Add following script on your Build section to mark CI job as failed when there is a false result, 

```
if grep false "$WORKSPACE/prototype/target/jmeter/results/*.jtl"; then
   echo "Test Failures!!! please check "$WORKSPACE/prototype/target/jmeter/results/*.jtl" file"
   exit 1
fi
```

Add following script on your Build section to mark CI job as failed when threshold is less than 1 (or number according to your business case) -

```
SUMMARY=${WORKSPACE}/prototype/target/jmeter/logs/*.log
grep "jmeter.reporters.Summariser: summary" ${SUMMARY} | tail -1 | awk '{print $12}' | cut -d "." -f1 |
awk '{if($0<=1){echo "Thoughput is less than 1 per sec" exit 1} }'
```
To generate JMeter dashbaord after test run use following [approach](https://www.youtube.com/watch?v=s7A0UxxD5zo) 
