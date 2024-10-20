## Callbacks

Here is a list with all the available Active Record callbacks, listed in the order in which they will get called during the respective operations:

* before_validation
* after_validation
* before_save
* around_save
* before_create
* around_create
* after_create
* after_save
* after_commit / after_rollback

### Callback Objects
Sometimes the callback methods that you'll write will be useful enough to be reused by other models. Active Record makes it possible to create classes that encapsulate the callback methods, so they can be reused.

Here's an example of an after_commit callback class to deal with the cleanup of discarded files on the filesystem. This behavior may not be unique to our PictureFile model and we may want to share it, so it's a good idea to encapsulate this into a separate class. This will make testing that behavior and changing it much easier.

```
class FileDestroyerCallback
  def after_commit(file)
    if File.exist?(file.filepath)
      File.delete(file.filepath)
    end
  end
end

```
When declared inside a class, as above, the callback methods will receive the model object as a parameter. This will work on any model that uses the class like so:

```
class PictureFile < ApplicationRecord
  after_commit FileDestroyerCallback.new
end
```
Note that we needed to instantiate a new FileDestroyerCallback object, since we declared our callback as an instance method. This is particularly useful if the callbacks make use of the state of the instantiated object. Often, however, it will make more sense to declare the callbacks as class methods:

```
class FileDestroyerCallback
  def self.after_commit(file)
    if File.exist?(file.filepath)
      File.delete(file.filepath)
    end
  end
end
```
When the callback method is declared this way, it won't be necessary to instantiate a new FileDestroyerCallback object in our model.

```
class PictureFile < ApplicationRecord
  after_commit FileDestroyerCallback
end
```