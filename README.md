# SDWebImage documentation
SDWebImage Documentation https://sdwebimage.github.io

This repository hosts the in source documentation for [SDWebImage](https://github.com/SDWebImage/SDWebImage) and its related projects. You can view this at [sdwebimage.github.io](https://sdwebimage.github.io).

## Maintenance

The documentation is auto-generated using [Jazzy](https://github.com/realm/jazzy).

#### Install jazzy

```
[sudo] gem install jazzy
```

#### Modify the contents

This documentation page now hosting both Core repo and other related framework's documentation. To modify the contents, just using the Markdown format and using jazzy to generate the HTML representation. Or directly modify the `index.html`.

#### Generate the SDWebImage documentation

+ Clone both [SDWebImage](https://github.com/SDWebImage/SDWebImage.git), [jazzy-theme](https://github.com/SDWebImage/jazzy-theme.git) and this repo
+ Place them in the same folder
+ Go the SDWebImage folder
+ Run the following command, remember to change the version string:

```
jazzy \
  --objc \
  --author SDWebImage \
  --github_url https://github.com/SDWebImage/SDWebImage \
  --github-file-prefix https://github.com/SDWebImage/SDWebImage/tree/5.9.0 \
  --module-version 5.9.0 \
  --umbrella-header WebImage/SDWebImage.h \
  --documentation=Docs/\*.md \
  --undocumented-text "" \
  --module SDWebImage \
  --framework-root . \
  --sdk iphonesimulator \
  --output ../sdwebimage.github.io/SDWebImage \
  --theme ../jazzy-theme/themes/apple
```

#### Generate SDWebImage related project documentation

SDWebImage now contains many related project, like the [Coder Plugins](https://github.com/SDWebImage/SDWebImage/wiki/Coder-Plugin-List) repo, the SwiftUI repo [SDWebImageSwiftUI](https://github.com/SDWebImage/SDWebImageSwiftUI).

You should place the generated documentation output folder, inside the sub-directory of this repo.

##### Swift

For Swift project, take SDWebImageSwiftUI for example:

```
jazzy \
  --author SDWebImageSwiftUI \
  --github_url https://github.com/SDWebImage/SDWebImageSwiftUI \
  --github-file-prefix https://github.com/SDWebImage/SDWebImageSwiftUI/tree/1.5.0 \
  --module-version 1.5.0 \
  --undocumented-text "" \
  --module SDWebImageSwiftUI \
  --framework-root . \
  --sdk iphonesimulator \
  --output ../sdwebimage.github.io/SDWebImageSwiftUI \
  --theme ../jazzy-theme/themes/apple
```

##### Objective-C

For Objective-C project, it's a little trick that you have to **fake** an umbrella header, make the include header search path, the same as folder structure. Take SDWebImagePhotosPlugin for example:

Move the `SDWebImagePhotosPlugin/Module/SDWebImagePhotosPlugin.h` -> `SDWebImagePhotosPlugin/SDWebImagePhotosPlugin.h`. Then modify all the include form, from this:

```objectivec
#import <SDWebImagePhotosPlugin/NSURL+SDWebImagePhotosPlugin.h>
```

to this:

```objectivec
#import "Classes/NSURL+SDWebImagePhotosPlugin.h"
// And, if there are no `#import <UIKit/UIKit.h>`, add this as well
```

Finally, use jazzy to generate the documentation:

```
jazzy \
  --objc \
  --author SDWebImagePhotosPlugin \
  --github_url https://github.com/SDWebImage/SDWebImagePhotosPlugin \
  --github-file-prefix https://github.com/SDWebImage/SDWebImagePhotosPlugin/tree/0.4.0 \
  --module-version 0.4.0 \
  --umbrella-header SDWebImagePhotosPlugin/SDWebImagePhotosPlugin.h \
  --undocumented-text "" \
  --module SDWebImagePhotosPlugin \
  --framework-root . \
  --sdk iphonesimulator \
  --output ../sdwebimage.github.io/SDWebImagePhotosPlugin \
  --theme ../jazzy-theme/themes/apple
```