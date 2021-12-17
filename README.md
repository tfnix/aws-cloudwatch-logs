## Amazon Cloudwatch 
***Gravando logs na AWS Cloudwatch*** <br>


Com shellscript

```bash

#!/bin/bash

LOGGROUP="logTest"
LOGSTREAM="anotherWorld"
REGION="us-east-2"
TIMESTAMP=`date "+%s%N" --utc`
TIMESTAMP=`expr $TIMESTAMP / 1000000`

# MESSAGE log sample
MESSAGE="[info] Server.js ha started"


SEQUENCETOKEN=$(aws logs describe-log-streams --log-group-name "$LOGGROUP" \
			--query 'logStreams[?logStreamName==`'$LOGSTREAM'`].[uploadSequenceToken]' \
			--output text)




if [ -z $SEQUENCETOKEN ] || [ $SEQUENCETOKEN == "None" ]; then
TOKENSENTENCE=""
else 
TOKENSENTENCE="--sequence-token $SEQUENCETOKEN" 
fi



aws logs put-log-events --log-group-name "$LOGGROUP" \
		         --log-stream-name "$LOGSTREAM" \
		         --log-events timestamp=$TIMESTAMP,message="\"$MESSAGE\"" \
		         $TOKENSENTENCE




```

Com NodeJs/Winston


```js
// ...
```

Referencias: <br>
https://aws.amazon.com/tools/ <br>
https://aws.amazon.com/cli/
