# VirtualKeyboardForQt
## Plugin installation
Copy "freevirtualkeyboardplugin.dll" to "C:\Qt\<6.*.*>\< mingw_64 or msvc2019_64>\plugins\platforminputcontexts"
Copy "FreeVirtualKeyboard" folder to "C:\Qt\<6.*.*>\< mingw_64 or msvc2019_64>\qml"

## Use the plugin in the project
On main.cpp add:
'''cpp
app.setProperty("QT_IM_MODULE", QVariant("freevirtualkeyboard"));
'''
On main.qml add:

'''cpp
    import QtQuick.FreeVirtualKeyboard
    //...
    InputPanel {
        id: inputPanel
        anchors.left: parent.left
        anchors.right: parent.right
        anchors.bottom: parent.bottom
        height: 250
        states: State {
            name: "visible"
            when: Qt.inputMethod.visible
            PropertyChanges {
                target: inputPanel
                y: window.height - inputPanel.height
            }
        }
        transitions: Transition {
            from: ""
            to: "visible"
            reversible: true
            ParallelAnimation {
                NumberAnimation {
                    properties: "y"
                    duration: 150
                    easing.type: Easing.InOutQuad
                }
            }
        }
    }
    '''
