# Remove-Foreign-Keys-from-Laravel-Model
Remove Foreign Keys from Laravel Model

```php

 $tableNames = Schema::getConnection()->getDoctrineSchemaManager()->listTableNames();

            $logs = [];
            foreach ($tableNames as $tableName) {
                return $foreignKeys = Schema::getConnection()->getDoctrineSchemaManager()->listTableForeignKeys($tableName);

                foreach ($foreignKeys as $foreignKey) {
                    //get the table name
                    $table = $foreignKey->getForeignTableName();
                    //remove the foreign key
                    Schema::table(
                        $tableName,
                        function (Blueprint $table) use ($foreignKey) {
                            $table->dropForeign($foreignKey->getName());
                        }
                    );
                    $logs[] = "Foreign key: " . $foreignKey->getName() . " references " . $foreignKey->getForeignTableName() . "." . implode(", ", $foreignKey->getForeignColumns());
                }
            }
            return response()->json(['status' => 'success', 'logs' => $logs], 200);

```
