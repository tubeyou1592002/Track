# مدل داده

دیتابیس: SQLite + SpatiaLite — یک فایل واحد برای همه پروژه‌ها.

## جداول

### projects
| ستون | نوع | توضیح |
|---|---|---|
| id | INTEGER PK | شناسه |
| title | TEXT | عنوان پروژه |
| crs_project | TEXT | CRS محاسبه (Lambert ایران) |
| crs_storage | TEXT | CRS ذخیره (WGS84) |
| default_max_range_m | REAL | برد پیش‌فرض (۱۰۰۰۰۰) |
| default_angle_accuracy_deg | REAL | دقت زاویه پیش‌فرض |
| active_target_id | INTEGER FK | هدف فعال |
| created_at | TEXT | زمان ایجاد (UTC) |

### observers
| ستون | نوع | توضیح |
|---|---|---|
| id | INTEGER PK | شناسه |
| project_id | INTEGER FK | پروژه |
| name | TEXT | نام ناظر |
| x_wgs84 | REAL | طول جغرافیایی |
| y_wgs84 | REAL | عرض جغرافیایی |
| elevation_m | REAL | ارتفاع (متر) |
| range_override_m | REAL | برد اختصاصی (nullable) |
| color | TEXT | رنگ |
| shape | TEXT | شکل |
| font_size | INTEGER | اندازه فونت |
| is_active_in_calc | BOOLEAN | فعال در محاسبه |
| created_at | TEXT | زمان ایجاد |

### targets
| ستون | نوع | توضیح |
|---|---|---|
| id | INTEGER PK | شناسه |
| project_id | INTEGER FK | پروژه |
| name | TEXT | نام هدف |
| color | TEXT | رنگ |
| created_at | TEXT | زمان ایجاد |

### observations
| ستون | نوع | توضیح |
|---|---|---|
| id | INTEGER PK | شناسه |
| project_id | INTEGER FK | پروژه |
| target_id | INTEGER FK | هدف |
| observer_id | INTEGER FK | ناظر |
| azimuth_deg | REAL | زاویه سمت |
| elevation_deg | REAL | زاویه ارتفاعی |
| angle_accuracy_deg | REAL | دقت (nullable) |
| timestamp_utc | TEXT | زمان ثبت |
| is_active | BOOLEAN | فعال |

### tracks
| ستون | نوع | توضیح |
|---|---|---|
| id | INTEGER PK | شناسه |
| target_id | INTEGER FK | هدف |
| computed_x | REAL | طول محاسبه‌شده |
| computed_y | REAL | عرض محاسبه‌شده |
| computed_z | REAL | ارتفاع محاسبه‌شده |
| error_radius_h_m | REAL | شعاع خطای افقی |
| error_vertical_m | REAL | خطای عمودی |
| timestamp_utc | TEXT | زمان محاسبه |
| status | TEXT | valid / low_accuracy / ambiguous / single_observer |

### settings
| ستون | نوع | توضیح |
|---|---|---|
| id | INTEGER PK | شناسه |
| project_id | INTEGER FK | پروژه |
| default_angle_accuracy | REAL | دقت پیش‌فرض |
| warn_angle_threshold_deg | REAL | آستانه هشدار (۵) |
| critical_angle_threshold_deg | REAL | آستانه بحرانی (۲) |
| interpolation_enabled | BOOLEAN | درون‌یابی |
| interpolation_method | TEXT | linear / catmull-rom |
| track_visible | BOOLEAN | نمایش مسیر |
| max_range_m | REAL | حداکثر برد |
| observer_color | TEXT | رنگ ناظر |
| target_color | TEXT | رنگ هدف |
| track_color | TEXT | رنگ مسیر |
| font_name | TEXT | فونت (Vazir) |
| font_size | INTEGER | اندازه فونت |
| log_level | TEXT | INFO / DEBUG |
| coordinate_format | TEXT | DD / DMS |
