## Must include initial sub text in macro as shown below ##

        Sub Blood_Flow_Velocity ()
	
## Data pad set up ##

        Call Doc.OpenView ("Data Pad")

        ' Begin DataPadColumnSetup
        Column = 2
        FunctionType = "Selection Duration"
        Channel = ##Blood Flow Velocity Channel##
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = 3
        FunctionType = "Selection Start"
        Channel = ##Blood Flow Velocity Channel##
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = ##Blood Flow Velocity Channel##
        FunctionType = "Selection End"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = ##Blood Flow Velocity Channel##
        FunctionType = "Mean"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = ##Blood Flow Velocity Channel##
        FunctionType = "Maximum Value"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = ##Blood Flow Velocity Channel##
        FunctionType = "Minimum Value"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = ##Blood Flow Velocity Channel##
        FunctionType = "Maximum - Minimum"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = ##Blood Flow Velocity Channel##
        FunctionType = "Full Comment Text"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup
        
## Turn Remaining Channels off ##

        ' Begin DataPadColumnSetup
        Column = 10
        FunctionType = "{00000000-0000-0000-0000-000000000000}-0"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = 11
        FunctionType = "{00000000-0000-0000-0000-000000000000}-0"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        ' Begin DataPadColumnSetup
        Column = 12
        FunctionType = "{00000000-0000-0000-0000-000000000000}-0"
        Channel = 3
        RecordMode = 1
        Options = ""
        Call Doc.DataPadColumnSetup (Column, FunctionType, Channel, RecordMode, Options)
        ' End DataPadColumnSetup

        Call Doc.OpenCloseWindow ("Data Pad", 1, False)
        
## Set cursor to beginning of data ##

        ' Begin SetSelection
        Set selobj = CreateObject("ADIChart.Selection")
        Call selobj.SetSelectionRange (0, 0, 0, 1)
        Call selobj.SetChannelRange (0, 1, -1)
        Call selobj.SetChannelRange (1, 1, -1)
        Call selobj.SetChannelRange (2, 1, -1)
        Call selobj.SetChannelRange (3, 1, -1)
        Call selobj.SetChannelRange (4, 1, -1)
        Call selobj.SetChannelRange (5, 1, -1)
        Call selobj.SetChannelRange (6, 1, -1)
        Call selobj.SetChannelRange (7, 1, -1)
        Call selobj.SetChannelRange (8, 1, -1)
        Doc.SelectionObject = selobj
        ' End SetSelection

        Call Doc.SetViewState ("Chart View", 1, 61488)
        
## Find comment or point in data file for data to begin ##

        ' Begin Find
        ChannelIndex = ##Blood Flow Velocity Channel##
        SetAction = kSetActivePoint
        SelectMode = kSelectAround
        SelectTime = 1
        DataDisplayMode = kViewDataVisible
        SelectAll = False
        Direction = kSearchForward
        FindType = "Search for comment"
        FindData = "JustThisChannel=0;WhatToLookFor=##Comment Name##;"
        Call Doc.Find (ChannelIndex, SetAction, SelectMode, SelectTime, DataDisplayMode, SelectAll, Direction, FindType, FindData)
        ' End Find
        
## Final local minima (diastolic blood flow velocity) ##

        ' Begin Find
        ChannelIndex = ##Blood Flow Velocity Channel##
        SetAction = kSetActivePoint
        SelectMode = kSelectAround
        SelectTime = 1
        DataDisplayMode = kViewDataVisible
        SelectAll = False
        Direction = kSearchForward
        FindType = "Local minima"
        FindData = "NoiseThreshold=0.01;"
        Call Doc.Find (ChannelIndex, SetAction, SelectMode, SelectTime, DataDisplayMode, SelectAll, Direction, FindType, FindData)
        ' End Find
        
## Set number of repitions for macro ##

        For i = 1 to ##Number for amount of times for macro to repeat##


          ' Begin Find
          ChannelIndex = ##Blood Flow Velocity Channel##
          SetAction = kSetToPreviousPoint
          SelectMode = kSelectAround
          SelectTime = 1
          DataDisplayMode = kViewDataVisible
          SelectAll = False
          Direction = kSearchForward
          FindType = "Local minima"
          FindData = "NoiseThreshold=0.01;"
          Call Doc.Find (ChannelIndex, SetAction, SelectMode, SelectTime, DataDisplayMode, SelectAll, Direction, FindType, FindData)
          ' End Find

          ' The function below will return true if the last operation failed, which will cause the current loop to exit
          Call Doc.AddToDataPad ()

        Next
        Call Doc.OpenView ("Data Pad")
        Call Doc.SetViewState ("Chart View", 1, 61728)
        

        End Sub
