I've written a helper API for loading and monitoring resources which is based upon an AS3 library called Queueloader (http://code.google.com/p/queueloader-as3/).  This AS2 version has the following features:

  * Individual monitoring
  * Overall queue monitoring
  * Image loading
  * SWF loading
  * MP3 loading

Example:
```
import com.fboyle.load.QueueLoader;
import com.fboyle.load.QueueLoaderEvent; 
 
var queue:QueueLoader = new QueueLoader();   
 
var infoOb:Object = new Object();
infoOb.id = "123456";   
 
queue.addItemAt("sample1.swf", _root.tmp, infoOb);
queue.addItemAt("sample2.swf", _root.tmp2, null);   
 
queue.execute();   
 
queue.addEventListener(QueueLoaderEvent.ITEM_PROGRESS, itemProgress);
queue.addEventListener(QueueLoaderEvent.ITEM_COMPLETE, itemComplete);
queue.addEventListener(QueueLoaderEvent.QUEUE_COMPLETE, queueComplete);   
queue.addEventListener(QueueLoaderEvent.QUEUE_PROGRESS, queueProgress);

 
function itemProgress(ev:Object):Void {
     trace(ev.file + ": " + ev.percent + "%");
}   
 
function itemComplete(ev:Object):Void {
     trace(ev.file+ " is loaded! (id - "+ ev.id + ")");
}   
 
function queueComplete(ev:Object):Void {
     trace("queue is complete----------");
}

function queueProgress(ev:Object):Void
{
	trace("Overall progress: " + ev.percent + " %");
}
```