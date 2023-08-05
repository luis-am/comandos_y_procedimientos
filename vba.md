## Macros

Esta macros sirve para que cuando añadamos o modificamos un registro en la tabla, este automáticamente se actualiza en la tabla dinámica.

	Private Sub Worksheet_Activate()
	ActiveSheet.PivotTables("reportes").PivotCache.Refresh
	End Sub

> En el {}, se pone el nombre de la tabla dinámica.
