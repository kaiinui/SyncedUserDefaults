![SyncedUserDefaults](https://dl.dropboxusercontent.com/u/7817937/_github/SyncedUserDefaultsLogo__.png)
====================

Syncable User Defaults

### Start synchronization service

```objc
[[SYNUserDefaultsService service] startWithKey:USER_SECRET_KEY];
```

### `NSUserDefaults` compatible interface

```objc
[[SYNUserDefaults defaults] setObject:@"Some value" forKey:@"somekey"];

[[SYNUserDefaults defaults] stringForKey:@"somekey"];
```

### Observing value change

```objc
[[SYNUserDefaults defaults] addObserver:self forKey:@"somekey"];
```

### `NSNotification` manner

```objc
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(userDefaultsDidChange:) name:kSYNUserDefaultsDidChangeNotification object:nil];

- (void)userDefaultsDidChange:(NSNotification *)notification {
    NSString *key = notification.userInfo[kSYNUserDefaultsKeyKey];
    id value = notification.userInfo[kSYNUserDefaultsValueKey];
}
```

### ReactiveCocoa manner

```objc
[[SYNUserDefaults rac_signalForKey:@"somekey"] subscribeNext:^(NSString *value) {
    // Do something with value.
}];
```

You can avoid circular reference with using `libextobjc`

```objc
@weakify(self);
[[SYNUserDefaults rac_signalForKey:@"somekey"] subscribeNext:^(NSString *value) {
    @strongify(self);
    // Do something with value and self.
}];
```

Status
---

WIP
