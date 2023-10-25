# 使用box同层级？/Tab可以访问

~~~text
tabIndex=-1  make Tab not work

tabIndex=0 make it sense
~~~

Ps: Using box make button and login in the same level and Tab on the keyboard can access the button (bug).

原因不明 套上box 也不管用

# Ntp時間設定

カメラ時間

Cameleo時間同期



~~~jsx
 {cameraTypeStrings[camera.camera.camera_type] + (camera.camera.camera_type === "gwbox" && camera.camera.gwbox && camera.camera.gwbox.name ? "(" + (camera.camera.gwbox.name) + ")" : "")}
~~~



~~~jsx
<TableCell
  sx={bodyCellProps}
  style={{
    overflowWrap: 'break-word',
  }}
>
 {(camera.camera.camera_type === "gwbox" && camera.camera.gwbox && camera.camera.gwbox.name ? (
      "GWBOXカメラ"　+ "(" + (camera.camera.gwbox.name) + ")" : ""
  )}
</TableCell>
~~~

