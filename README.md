# SilverStripe Image Minify Module

SS-image-min is a Silverstripe module for image compressing and server-side caching based on [nielse63/php-image-cache](https://github.com/nielse63/php-image-cache).

## Requirements

Tested on SilverStrip 3.1

## Instalation

After installing the module by any of the following methods you must build you database by visiting http://yoursite.com/dev/build.

### Composer

Soon....

### Github

Navigate to the root directory of your SilverStripe application and execute `git clone https://github.com/encoda/ss-image-min.git`

### Manually

Download [this zip file](https://github.com/encoda/ss-image-min/zipball/master) and extract it in your SilverStripe root directory.

## Usage

Once the module is installed, a compressed cache version of each Silverstripe `Image` instance file is automatically generated by the time it is saved in the database, or (if the module is lately installed in the application and there are already several images in the database) individually at the moment the URL of any of them is called directly or indirectly, by calling either one of its following methods: `getTag`, `getUrl` or `getAbsoluteURL`.

### Example

mysite/code/NarcissisticTeenager.php

``` php
<?php

NarcissisticTeenager extends DataObject {
    ...
    private static $many_many = array(
        'Selfies' => 'Image',
    );

    public function FirstSelfie() {
        return $this->Selfies()->First();
    }
    ...
}
```

themes/autinpack/templates/Page.ss

``` ss
<% with $SomeNarcissisticTeenager %>
    <% loop $Selfies %>
        $GetTag
    <% end_loop %>
<% end_with %>
```

## Configuration

SS-image-min doesn't require any configuration.
Although you can overwrite some of them through your `_config.php`.

### Compress Rate

**Default:** `80`

```
<?php

SSImageCache::$compress_rate = 70;
```

### Increasead Memory Limit

Generating compressed images uses a lot more than the PHP is normally allowed to use. So, by default, SS-image-min increases its memory limit temporarily during the compression processes.

**Default:** '2480M'

```
<?php

SSImageCache::$increased_memory_limit = '128M';
```

## License (MIT)

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
