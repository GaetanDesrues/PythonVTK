# PythonVTK
Documentation/Memo for handling python package for vtk unstructured grid

    import vtk

    reader = vtk.vtkUnstructuredGridReader()
    reader.SetFileName("file.vtk")
    reader.Update()
    output = reader.GetOutput()
    
    
    c = output.GetCell(5) # cell of id 5
    id = c.GetPointId(0) # id of the first vertex in the cell c
    pos = output.GetPoint(id) # position of the point id
    
    
    cells = output.GetCells()
    cells = vtk.vtkCellArray() # Empty cells list
    
    output.GetNumberOfCells()
    output.GetCellType(cellId)
    
    cellData = output.GetCellData()
    
    from vtk.util import numpy_support
    import numpy as np
    dataArray = numpy_support.numpy_to_vtk(cT) # np.array() to vtk array
    dataArray.SetName("field") # Name as it will appear in the vtk after FIELD
    cellData.AddArray(dataArray)
    
    
    output.SetCells(types, cells)
    
    writer = vtk.vtkUnstructuredGridWriter()
    writer.SetFileName("file_modified.vtk") # writer.GetFileName()
    writer.SetInputData(output)
    writer.Write()
    
    
    
    # Add a cell
    def addTri(cells, types, ids):
      types.append(5)

      triangle = vtk.vtkTriangle() # vtk.vtkTetra() ...
      triangle.GetPointIds().SetId(0,ids[0])
      triangle.GetPointIds().SetId(1,ids[1])
      triangle.GetPointIds().SetId(2,ids[2])

      cells.InsertNextCell(triangle)
