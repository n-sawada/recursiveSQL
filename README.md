# recursiveSQL

    NSArray *tags = @[@1, @2, @3];
    
    NSString *sql =
    @"\
    SELECT\
    *\
    FROM\
    A as a,\
    B as b\
    WHERE\
    a.id = ?\
    AND\
    b.selected = 1\
    ";
    
    NSString *rappedUpperSql = @"SELECT * FROM (";
    NSString *rappedLowerSql = @") as a, B as b WHERE a.id = ?";
    
    __block NSString *recurrenceSql = nil;
    
    [tags enumerateObjectsUsingBlock:^(id  _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
        if (idx == 0) {
            recurrenceSql = sql;
            return ;
        }
        
        recurrenceSql = [rappedUpperSql stringByAppendingFormat:@"%@%@", recurrenceSql, rappedLowerSql];
    }];
    

    NSLog(@"%@", recurrenceSql );
