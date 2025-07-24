# ドキュメント・テストケース

本文書は、テストケースの自動生成をサポートする。

すべての有効な IDS 実装は、提供されたテストケースの期待値に対して同一の動作を示さなければならない。

これは、IFC検証の期待される動作を記述するためのものであり、期待される実装から曖昧さを取り除くために、すべての標準的なケースとエッジケースをカバーする必要がある。

テストケースは、テーマ別（属性、エンティティなど）にフォルダ分けされ、一致するIFC/IDSカップルの検証結果に応じて、3つのグループ（合格、不合格、無効など）に整理される。

| ファイル名接頭辞 | 記述 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| パス | すべての要件を満たす |
| 失敗 | 少なくとも1つの要件が不合格 |
| 無効 | 少なくとも1つの要件が不合格（無効なファイルは監査ツールに準拠していないため、IFCの内容に関係なく、要件を満たすことができない） |

IDS files are generated from the data of this script executing the `CreateTestCases` target in the repository.

IFCファイルは、以前に行われた作業からインポートされたものである。[IfcOpenShellリポジトリ](https://blenderbim.org/docs-python/ifctester.html)そして適切な場合には、それを採用する。

## 属性

### 禁止ファセットは必須ファセットの反対を返す

``` ids attribute/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
IFC2X3 IFC4 IFC4X3_ADD2
Entity: ''IFCWALL''
Requirements:
Attribute: Prohibited,''Name''
```

### 必須ファセットは、通常通りすべてのパラメータをチェックする。

``` ids attribute/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### オプションの属性は、指定された場合に渡されます。

``` ids attribute/pass-an_optional_attribute_passes_if_specified.ids
An optional attribute passes if specified
Entity: ''IFCWALL''
Requirements:
Attribute: Optional,''Name'', ''Foobar''
```

### オプションの属性は、NULLの場合に渡されます。

``` ids attribute/pass-an_optional_attribute_passes_if_null.ids
An optional attribute passes if null
Entity: ''IFCWALL''
Requirements:
Attribute: Optional,''Name'', ''Foobar''
```

### オプションの属性は、空の場合は失敗します。

``` ids attribute/fail-an_optional_attribute_fails_if_empty.ids
An optional attribute fails if empty
Entity: ''IFCWALL''
Requirements:
Attribute: Optional,''Name'', ''Foobar''
```

### 属性はオカレンスに継承されない

``` ids attribute/fail-attributes_are_not_inherited_by_the_occurrence.ids
Attributes are not inherited by the occurrence
Entity: ''IFCWALL''
Requirements:
Attribute: ''Description'',''Foobar''
```

### オブジェクトを参照する属性は

``` ids attribute/pass-attributes_referencing_an_object_should_pass.ids
Attributes referencing an object should pass
IFC4
Entity: ''IFCTASK''
Requirements:
Attribute: ''TaskTime''
```

### 属性は大文字と小文字を区別して文字列をチェックすべきである 1/2

``` ids attribute/pass-attributes_should_check_strings_case_sensitively_1_2.ids
Attributes should check strings case sensitively 1/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Foobar''
```

### 属性は大文字と小文字を区別して文字列をチェックすべきである。

``` ids attribute/fail-attributes_should_check_strings_case_sensitively_2_2.ids
Attributes should check strings case sensitively 2/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Foobar''
```

### 真偽値がfalseの属性はパスする必要があります。

``` ids attribute/pass-attributes_with_a_boolean_false_should_pass.ids
Attributes with a boolean false should pass
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''IsCritical''
```

### 真偽値trueを持つ属性は、以下を渡す必要があります。

``` ids attribute/pass-attributes_with_a_boolean_true_should_pass.ids
Attributes with a boolean true should pass
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''IsCritical''
```

### 論理的に未知の属性は常に失敗する

``` ids attribute/fail-attributes_with_a_logical_unknown_always_fail.ids
Attributes with a logical unknown always fail
Entity: ''IFCPRESENTATIONLAYERWITHSTYLE''
Requirements:
Attribute: ''LayerOn''
```

### プリミティブを参照するselectを持つ属性は、以下を渡す必要があります。

``` ids attribute/pass-attributes_with_a_select_referencing_a_primitive_should_pass.ids
Attributes with a select referencing a primitive should pass
Entity: ''IFCSURFACESTYLERENDERING''
Requirements:
Attribute: ''DiffuseColour''
```

### オブジェクトを参照するselectを持つ属性は、以下を渡す必要があります。

``` ids attribute/pass-attributes_with_a_select_referencing_an_object_should_pass.ids
Attributes with a select referencing an object should pass
Entity: ''IFCSURFACESTYLERENDERING''
Requirements:
Attribute: ''DiffuseColour''
```

### 文字列値を持つ属性は

``` ids attribute/pass-attributes_with_a_string_value_should_pass.ids
Attributes with a string value should pass
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### 持続時間がゼロの属性はパスすべきである。

``` ids attribute/pass-attributes_with_a_zero_duration_should_pass.ids
Attributes with a zero duration should pass
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''ScheduleDuration''
```

### 数字がゼロの属性は意味があり、パスすべきである。

``` ids attribute/pass-attributes_with_a_zero_number_have_meaning_and_should_pass.ids
Attributes with a zero number have meaning and should pass
Entity: ''IFCQUANTITYCOUNT''
Requirements:
Attribute: ''CountValue''
```

### 空のリストを持つ属性は常に失敗する

``` ids attribute/fail-attributes_with_an_empty_list_always_fail.ids
Attributes with an empty list always fail
Entity: ''IFCRELCONNECTSPATHELEMENTS''
Requirements:
Attribute: ''RelatingPriorities''
```

### 空の集合を持つ属性は常に失敗する

``` ids attribute/fail-attributes_with_an_empty_set_always_fail.ids
Attributes with an empty set always fail
Entity: ''IFCPRESENTATIONLAYERWITHSTYLE''
Requirements:
Attribute: ''LayerStyles''
```

### 空文字列を含む属性は常に失敗する

``` ids attribute/fail-attributes_with_empty_strings_always_fail.ids
Attributes with empty strings always fail
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### NULL値を持つ属性は常に失敗する

``` ids attribute/fail-attributes_with_null_values_always_fail.ids
Attributes with null values always fail
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### ブール値は小文字の文字列で指定する必要があります。

``` ids attribute/fail-booleans_must_be_specified_as_lowercase_strings_1_3.ids
Booleans must be specified as lowercase strings 1/3
Entity: ''IFCTASK''
Requirements:
Attribute: ''IsMilestone'',''true''
```

### ブーリアンは小文字の文字列として指定しなければならない。

``` ids attribute/invalid-booleans_must_be_specified_as_lowercase_strings_2_3.ids
Booleans must be specified as lowercase strings 2/3
Entity: ''IFCTASK''
Requirements:
Attribute: ''IsMilestone'',''FALSE''
```

### ブーリアンは小文字の文字列として指定しなければならない。

``` ids attribute/pass-booleans_must_be_specified_as_lowercase_strings_3_3.ids
Booleans must be specified as lowercase strings 3/3
Entity: ''IFCTASK''
Requirements:
Attribute: ''IsMilestone'',''false''
```

### 日付は文字列として扱われる 1/2

``` ids attribute/fail-dates_are_treated_as_strings_1_2.ids
Dates are treated as strings 1/2
IFC4
Entity: ''IFCCLASSIFICATION''
Requirements:
Attribute: ''EditionDate'',''2022-01-01''
```

### 日付は文字列として扱われる 2/2

``` ids attribute/pass-dates_are_treated_as_strings_2_2.ids
Dates are treated as strings 2/2
IFC4
Entity: ''IFCCLASSIFICATION''
Requirements:
Attribute: ''EditionDate'',''2022-01-01''
```

### 派生属性はチェックできず、常に失敗する

``` ids attribute/invalid-derived_attributes_cannot_be_checked_and_always_fail.ids
Derived attributes cannot be checked and always fail
Entity: ''IFCCARTESIANPOINT''
Requirements:
Attribute: ''Dim''
```

### 持続時間は文字列として扱われる 1/2

``` ids attribute/pass-durations_are_treated_as_strings_1_2.ids
Durations are treated as strings 1/2
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''ScheduleDuration'',''PT16H''
```

### デュレーションはストリングス2/2として扱われる

``` ids attribute/fail-durations_are_treated_as_strings_2_2.ids
Durations are treated as strings 2/2
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''ScheduleDuration'',''PT16H''
```

### GlobalIds は文字列として扱われ、展開されない。

``` ids attribute/pass-globalids_are_treated_as_strings_and_not_expanded.ids
GlobalIds are treated as strings and not expanded
Entity: ''IFCWALL''
Requirements:
Attribute: ''GlobalId'',''1hqIFTRjfV6AWq_bMtnZwI''
```

### IDSは識別子のような文字列の切り捨てを扱わない

``` ids attribute/fail-ids_does_not_handle_string_truncation_such_as_for_identifiers.ids
IDS does not handle string truncation such as for identifiers
IFC4
Entity: ''IFCPERSON''
Requirements:
Attribute: ''Identification'',''123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345_extra_characters''
```

### 整数は数値と同じ規則に従う

``` ids attribute/pass-integers_follow_the_same_rules_as_numbers.ids
Integers follow the same rules as numbers
IFC4
Entity: ''IFCSTAIRFLIGHT''
Requirements:
Attribute: ''NumberOfRisers'',''42''
```

### 整数を浮動小数点数で表すことはできない 2/2

``` ids attribute/invalid-integers_cannot_be_expressed_as_floating_point_numbers_2_2.ids
Integers cannot be expressed as floating point numbers 2/2
IFC4
Entity: ''IFCSTAIRFLIGHT''
Requirements:
Attribute: ''NumberOfRisers'',''42.0''
```

### 無効な属性名は常に失敗する

IFCWALL タイプのエンティティは ActingRole 属性を持ちません。

``` ids attribute/invalid-invalid_attribute_names_always_fail.ids
Invalid attribute names always fail
Entity: ''IFCWALL''
Requirements:
Attribute: ''ActingRole''
```

### 逆属性はチェックできず、常に失敗する

``` ids attribute/invalid-inverse_attributes_cannot_be_checked_and_always_fail.ids
Inverse attributes cannot be checked and always fail
Entity: ''IFCPERSON''
Requirements:
Attribute: ''EngagedIn''
```

### 名前の制限は、どのような結果にもマッチする

``` ids attribute/pass-name_restrictions_will_match_any_result_1_3.ids
Name restrictions will match any result 1/3
Entity: ''IFCMATERIALLAYERSET''
Requirements:
Attribute: Pattern(''.*Name.*'')
```

### 名前の制限は、2/3 のすべての結果と一致する。

``` ids attribute/pass-name_restrictions_will_match_any_result_2_3.ids
Name restrictions will match any result 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: Enumeration(''Name'',''Description'')
```

### 名前の制限は、どのような結果にもマッチする 3/3

``` ids attribute/pass-name_restrictions_will_match_any_result_3_3.ids
Name restrictions will match any result 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: Enumeration(''Name'',''Description'')
```

### 非アスキー文字はエンコードなしで扱われる

``` ids attribute/pass-non_ascii_characters_are_treated_without_encoding.ids
Non-ascii characters are treated without encoding
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''♫Don'tÄrgerhôtelЊет''
```

### 数値のチェックには型キャストを使用します。

``` ids attribute/pass-numeric_values_are_checked_using_type_casting_1_4.ids
Numeric values are checked using type casting 1/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42''
```

### 数値は型キャストを使用してチェックされます。

``` ids attribute/pass-numeric_values_are_checked_using_type_casting_2_4.ids
Numeric values are checked using type casting 2/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42.''
```

### 数値のチェックには型キャストを使用します。

``` ids attribute/pass-numeric_values_are_checked_using_type_casting_3_4.ids
Numeric values are checked using type casting 3/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42.0''
```

### 数値は型キャストを用いてチェックされる 4/4

``` ids attribute/fail-numeric_values_are_checked_using_type_casting_4_4.ids
Numeric values are checked using type casting 4/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42''
```

### 特別にフォーマットされた数字だけが許される 1/4

``` ids attribute/invalid-only_specifically_formatted_numbers_are_allowed_1_4.ids
Only specifically formatted numbers are allowed 1/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42,3''
```

### 特別にフォーマットされた数字のみが許される 2/4

``` ids attribute/invalid-only_specifically_formatted_numbers_are_allowed_2_4.ids
Only specifically formatted numbers are allowed 2/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''123,4.5''
```

### 特別にフォーマットされた数字だけが許される 3/4

``` ids attribute/pass-only_specifically_formatted_numbers_are_allowed_3_4.ids
Only specifically formatted numbers are allowed 3/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''1.2345e3''
```

### 特別にフォーマットされた数字のみが許される 4/4

``` ids attribute/pass-only_specifically_formatted_numbers_are_allowed_4_4.ids
Only specifically formatted numbers are allowed 4/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''1.2345E3''
```

### 値が整数である場合にfloatを指定するのは無効である。

属性名`NumberOfRiser`に改名された。`NumberOfRisers`IFC4

``` ids attribute/invalid-specifying_a_float_when_the_value_is_an_integer_is_invalid.ids
Specifying a float when the value is an integer is invalid
IFC4
Entity: ''IFCSTAIRFLIGHT''
Requirements:
Attribute: Pattern(''NumberOfRiser(s)?''),''42.3''
```

### 厳密な数値チェックは、境界制限を設けて行うことができる。

``` ids attribute/pass-strict_numeric_checking_may_be_done_with_a_bounds_restriction.ids
Strict numeric checking may be done with a bounds restriction
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''42'') MaxInclusive(''42'')
```

### 型キャスト・チェックは列挙の制限内でも行われる。

列挙で定義される型は、dataTypeと互換性がある必要がある。
For attribute facets, the dataType is taken from the IDS schema.

ロードマップ：一貫性のないタイプは、監査ツールによって把握されるべきである。

``` ids attribute/pass-typecast_checking_may_also_occur_within_enumeration_restrictions.ids
Typecast checking may also occur within enumeration restrictions
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double Enumeration(''42'',''43'')
```

### リストの値チェックは常に失敗する

``` ids attribute/invalid-value_checks_always_fail_for_lists.ids
Value checks always fail for lists
Entity: ''IFCCARTESIANPOINT''
Requirements:
Attribute: ''Coordinates'',''Foobar''
```

### オブジェクトの値チェックは常に失敗する

``` ids attribute/invalid-value_checks_always_fail_for_objects.ids
Value checks always fail for objects
IFC4
Entity: ''IFCTASK''
Requirements:
Attribute: ''TaskTime'',''Foobar''
```

### セレクトの値チェックは常に失敗する

``` ids attribute/invalid-value_checks_always_fail_for_selects.ids
Value checks always fail for selects
Entity: ''IFCSURFACESTYLERENDERING''
Requirements:
Attribute: ''DiffuseColour'',''Foobar''
```

### 値の制限を使用することができる 1/3

``` ids attribute/pass-value_restrictions_may_be_used_1_3.ids
Value restrictions may be used 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 値による制限を受けることがある。

``` ids attribute/pass-value_restrictions_may_be_used_2_3.ids
Value restrictions may be used 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 値による制限あり 3/3

``` ids attribute/fail-value_restrictions_may_be_used_3_3.ids
Value restrictions may be used 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

## 分類

### データのない分類ファセットは、どの分類にもマッチする 1/2

``` ids classification/fail-a_classification_facet_with_no_data_matches_any_classification_1_2.ids
A classification facet with no data matches any classification 1/2
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+'')
```

### データのない分類ファセットは、どの分類にもマッチする 2/2

``` ids classification/pass-a_classification_facet_with_no_data_matches_any_classification_2_2.ids
A classification facet with no data matches any classification 2/2
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+'')
```

### 禁止ファセットは必須ファセットの反対を返す

``` ids classification/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCSLAB''
Requirements:
Classification: Prohibited,Pattern(''\w+'')
```

### 禁止された分類参照は、必須ファセットの反対を返す

``` ids classification/fail-a_prohibited_classification_reference_returns_the_opposite_of_a_required_facet.ids
A prohibited classification reference returns the opposite of a required facet
Entity: ''IFCSLAB''
Requirements:
Classification: Prohibited,''Foobar'',''1''
```

### 必須ファセットは、通常通りすべてのパラメータをチェックする。

``` ids classification/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+'')
```

### 要求される分類システムは、一致するものがなければ失敗する。

``` ids classification/fail-a_required_classification_system_fails_if_no_match.ids
A required classification system fails if no match
Entity: ''IFCSLAB''
Requirements:
Classification: ''Foobar1''
```

### オプションの分類値は、指定された場合に渡されます。

``` ids classification/pass-an_optional_classification_value_passes_if_specified.ids
An optional classification value passes if specified
Entity: ''IFCWALL''
Requirements:
Classification: Optional,Pattern(''\w+''),''ExpectedValue''
```

### nullの場合、オプションの分類値が渡される

``` ids classification/pass-an_optional_classification_value_passes_if_null.ids
An optional classification value passes if null
Entity: ''IFCWALL''
Requirements:
Classification: Optional,Pattern(''\w+''),''ExpectedValue''
```

### オプションの分類値は、マッチしない場合に失敗します。

``` ids classification/fail-an_optional_classification_value_fails_if_no_match.ids
An optional classification value fails if no match
Entity: ''IFCWALL''
Requirements:
Classification: Optional,Pattern(''\w+''),''ExpectedValue''
```

### 1/2を指定する場合は、システムと値の両方が一致しなければならない（すべて、いずれかではない）。

``` ids classification/pass-both_system_and_value_must_match__all__not_any__if_specified_1_2.ids
Both system and value must match (all, not any) if specified 1/2
Entity: ''IFCSLAB''
Requirements:
Classification: ''Foobar'',''1''
```

### 2/2を指定する場合は、システムと値の両方が一致しなければならない（すべてであって、いずれかではない）。

``` ids classification/fail-both_system_and_value_must_match__all__not_any__if_specified_2_2.ids
Both system and value must match (all, not any) if specified 2/2
Entity: ''IFCCOLUMN''
Requirements:
Classification: ''Foobar'',''1''
```

### 外部分類参照を持つルート化されていないリソースも、次のように渡す必要があります。

ifc4以降、IFCEXTERNALREFERENCERELATIONSHIPはIFCEXTERNALREFERENCEを任意のIFCRESOURCEOBJECTSELECTに関連付けることができる。

``` ids classification/pass-non_rooted_resources_that_have_external_classification_references_should_also_pass.ids
Non-rooted resources that have external classification references should also pass
IFC4
Entity: ''IFCMATERIAL''
Requirements:
Classification: Pattern(''\w+''),''1''
```

### 発生はシステムごとのタイプ分類を上書きする 1/3

``` ids classification/pass-occurrences_override_the_type_classification_per_system_1_3.ids
Occurrences override the type classification per system 1/3
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+''),''11''
```

### 発生はシステムごとのタイプ分類を上書きする 2/3

``` ids classification/fail-occurrences_override_the_type_classification_per_system_2_3.ids
Occurrences override the type classification per system 2/3
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+''),''22''
```

### 発生は、システム3/3によるタイプ分類をオーバーライドする。

``` ids classification/pass-occurrences_override_the_type_classification_per_system_3_3.ids
Occurrences override the type classification per system 3/3
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+''),''X''
```

### システム1/2に制限をかけることができる

``` ids classification/fail-restrictions_can_be_used_for_systems_1_2.ids
Restrictions can be used for systems 1/2
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''Foo.*'')
```

### システム2/2に使用できる制限

``` ids classification/pass-restrictions_can_be_used_for_systems_2_2.ids
Restrictions can be used for systems 2/2
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''Foo.*'')
```

### 値に制限をかけることができる 1/3

``` ids classification/pass-restrictions_can_be_used_for_values_1_3.ids
Restrictions can be used for values 1/3
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+''),Pattern(''1.*'')
```

### 2/3の値に制限をかけることができる。

``` ids classification/pass-restrictions_can_be_used_for_values_2_3.ids
Restrictions can be used for values 2/3
Entity: ''IFCCOLUMN''
Requirements:
Classification: Pattern(''\w+''),Pattern(''1.*'')
```

### 3/3の値に制限をかけることができる。

``` ids classification/fail-restrictions_can_be_used_for_values_3_3.ids
Restrictions can be used for values 3/3
Entity: ''IFCBEAM''
Requirements:
Classification: Pattern(''\w+''),Pattern(''1.*'')
```

### システムは正確に1/5に一致する必要がある

``` ids classification/pass-systems_should_match_exactly_1_5.ids
Systems should match exactly 1/5
Entity: ''IFCPROJECT''
Requirements:
Classification: ''Foobar''
```

### システムは2/5で正確に一致すること

``` ids classification/fail-systems_should_match_exactly_2_5.ids
Systems should match exactly 2/5
Entity: ''IFCWALL''
Requirements:
Classification: ''Foobar''
```

### システムは3/5で正確に一致すること

``` ids classification/pass-systems_should_match_exactly_3_5.ids
Systems should match exactly 3/5
Entity: ''IFCSLAB''
Requirements:
Classification: ''Foobar''
```

### システムは4/5で正確に一致すること

``` ids classification/pass-systems_should_match_exactly_4_5.ids
Systems should match exactly 4/5
Entity: ''IFCCOLUMN''
Requirements:
Classification: ''Foobar''
```

### システムは5/5に正確に一致すべきである

``` ids classification/pass-systems_should_match_exactly_5_5.ids
Systems should match exactly 5/5
Entity: ''IFCBEAM''
Requirements:
Classification: ''Foobar''
```

### 完全な分類が使用されている場合、値はサブリファレンスと一致する（例：EF_25_10はEF_25_10_25、EF_25_10_30などと一致するはず）

``` ids classification/pass-values_match_subreferences_if_full_classifications_are_used__e_g__ef_25_10_should_match_ef_25_10_25__ef_25_10_30__etc_.ids
Values match subreferences if full classifications are used (e.g. EF_25_10 should match EF_25_10_25, EF_25_10_30, etc)
Entity: ''IFCBEAM''
Requirements:
Classification: Pattern(''\w+''),''2''
```

### 軽量級を使用する場合、値は正確に一致する必要がある。

``` ids classification/pass-values_should_match_exactly_if_lightweight_classifications_are_used.ids
Values should match exactly if lightweight classifications are used
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+''),''1''
```

## エンティティ

### 一致するエンティティは

``` ids entity/pass-a_matching_entity_should_pass.ids
A matching entity should pass
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL''
```

### 一致する定義済みの型は、次のように渡す必要がある。

``` ids entity/pass-a_matching_predefined_type_should_pass.ids
A matching predefined type should pass
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''SOLIDWALL''
```

### NULLの定義済み型は、常に指定された定義済み型に失敗するはずである。

``` ids entity/fail-a_null_predefined_type_should_always_fail_a_specified_predefined_types.ids
A null predefined type should always fail a specified predefined types
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''SOLIDWALL''
```

### 列挙の定義済み型は大文字でなければならない。

``` ids entity/fail-a_predefined_type_from_an_enumeration_must_be_uppercase.ids
A predefined type from an enumeration must be uppercase
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''solidwall''
```

### 定義済みの型は、ユーザー定義の要素型を指定することができる。

``` ids entity/pass-a_predefined_type_may_specify_a_user_defined_element_type.ids
A predefined type may specify a user-defined element type
Entity: ''IFCWALLTYPE''
Requirements:
Entity: ''IFCWALLTYPE'',''WALDO''
```

### ユーザー定義の定義済みタイプを指定できる

``` ids entity/pass-userdefined_predefined_types_may_be_specified.ids
Userdefined predefined types may be specified
Entity: ''IFCWALLTYPE''
Requirements:
Entity: ''IFCWALLTYPE'',''USERDEFINED''
```

### 定義済みの型は、ユーザー定義のオブジェクト型を指定することができる。

列挙でカスタムが許可されている場合、このカスタムサブタイプは許可されるべきである。
IfcWall does not have predefinedType in 2X3, so the test case is constrained to IFC4

``` ids entity/pass-a_predefined_type_may_specify_a_user_defined_object_type.ids
A predefined type may specify a user-defined object type
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''WALDO''
```

### 定義済みの型は、ユーザー定義のプロセス型を指定することができる。

``` ids entity/pass-a_predefined_type_may_specify_a_user_defined_process_type.ids
A predefined type may specify a user-defined process type
IFC4
Entity: ''IFCTASKTYPE''
Requirements:
Entity: ''IFCTASKTYPE'',''TASKY''
```

### 指定された定義済みの型に一致しないエンティティは失敗します。

``` ids entity/fail-an_entity_not_matching_a_specified_predefined_type_will_fail.ids
An entity not matching a specified predefined type will fail
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''SOLIDWALL''
```

### 指定されたクラスに一致しないエンティティは失敗する

``` ids entity/invalid-an_entity_not_matching_the_specified_class_should_fail.ids
An entity not matching the specified class should fail
Entity: ''IFCSLAB''
Requirements:
Entity: ''IFCWALL''
```

### 一致するエンティティは、定義済みの型に関係なくパスする必要があります。

``` ids entity/pass-an_matching_entity_should_pass_regardless_of_predefined_type.ids
An matching entity should pass regardless of predefined type
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL''
```

### エンティティは、XSD 正規表現パターン 1/2 として指定できます。

``` ids entity/invalid-entities_can_be_specified_as_a_xsd_regex_pattern_1_2.ids
Entities can be specified as a XSD regex pattern 1/2
Entity: ''IFCWALL''
Requirements:
Entity: Pattern(''IFC.*TYPE'')
```

### エンティティは XSD 正規表現パターンとして指定できる 2/2

``` ids entity/pass-entities_can_be_specified_as_a_xsd_regex_pattern_2_2.ids
Entities can be specified as a XSD regex pattern 2/2
Entity: ''IFCWALLTYPE''
Requirements:
Entity: Pattern(''IFC.*TYPE'')
```

### エンティティは列挙として指定できる 1/3

``` ids entity/pass-entities_can_be_specified_as_an_enumeration_1_3.ids
Entities can be specified as an enumeration 1/3
Entity: ''IFCWALL''
Requirements:
Entity: Enumeration(''IFCWALL'',''IFCSLAB'')
```

### エンティティは列挙として指定できる 2/3

``` ids entity/pass-entities_can_be_specified_as_an_enumeration_2_3.ids
Entities can be specified as an enumeration 2/3
Entity: ''IFCSLAB''
Requirements:
Entity: Enumeration(''IFCWALL'',''IFCSLAB'')
```

### エンティティは列挙として指定できる 3/3

``` ids entity/invalid-entities_can_be_specified_as_an_enumeration_3_3.ids
Entities can be specified as an enumeration 3/3
Entity: ''IFCBEAM''
Requirements:
Entity: Enumeration(''IFCWALL'',''IFCSLAB'')
```

### エンティティは大文字の文字列で指定する必要があります。

``` ids entity/invalid-entities_must_be_specified_as_uppercase_strings.ids
Entities must be specified as uppercase strings
Entity: ''IFCWALL''
Requirements:
Entity: ''IfcWall''
```

### 継承された定義済み型は

``` ids entity/pass-inherited_predefined_types_should_pass.ids
Inherited predefined types should pass
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''X''
```

### 無効なエンティティは常に失敗する

``` ids entity/invalid-invalid_entities_always_fail.ids
Invalid entities always fail
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCRABBIT''
```

### オーバーライドされた定義済みの型は

``` ids entity/pass-overridden_predefined_types_should_pass.ids
Overridden predefined types should pass
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''X''
```

### 定義済みのタイプに制限を指定できる 1/3

``` ids entity/pass-restrictions_can_be_specified_for_the_predefined_type_1_3.ids
Restrictions can be specified for the predefined type 1/3
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',Pattern(''FOO.*'')
```

### 定義済みのタイプ2/3に制限を指定することができる。

``` ids entity/pass-restrictions_can_be_specified_for_the_predefined_type_2_3.ids
Restrictions can be specified for the predefined type 2/3
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',Pattern(''FOO.*'')
```

### 事前に定義されたタイプ3/3に制限を指定することができる。

``` ids entity/fail-restrictions_can_be_specified_for_the_predefined_type_3_3.ids
Restrictions can be specified for the predefined type 3/3
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',Pattern(''FOO.*'')
```

### サブクラスは一致するとはみなされない

``` ids entity/invalid-subclasses_are_not_considered_as_matching.ids
Subclasses are not considered as matching
Entity: ''IFCWALLSTANDARDCASE''
Requirements:
Entity: ''IFCWALL''
```

### ユーザー定義型は大文字と小文字を区別してチェックされる

``` ids entity/fail-user_defined_types_are_checked_case_sensitively.ids
User-defined types are checked case sensitively
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''WALDO''
```

## 子供たち

### ミニマムIDはミニマムifcをチェックできる (1/2)

``` ids ids/fail-a_minimal_ids_can_check_a_minimal_ifc_1_2.ids
A minimal ids can check a minimal ifc (1/2)
IFC4
Optional
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 最小のIDは、最小のifc (2/2)をチェックすることができる。

``` ids ids/pass-a_minimal_ids_can_check_a_minimal_ifc_2_2.ids
A minimal ids can check a minimal ifc (2/2)
IFC4
Optional
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### すべての要件が合格した場合にのみ、仕様が合格となる (1/2)

``` ids ids/fail-a_specification_passes_only_if_all_requirements_pass_1_2.ids
A specification passes only if all requirements pass (1/2)
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
Attribute: ''Description'',''Foobar''
```

### すべての要件が合格した場合のみ、仕様が合格となる (2/2)

``` ids ids/pass-a_specification_passes_only_if_all_requirements_pass_2_2.ids
A specification passes only if all requirements pass (2/2)
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
Attribute: ''Description'',''Foobar''
```

### 該当するものがない場合でも、オプション仕様で合格となる場合がある。

``` ids ids/pass-optional_specifications_may_still_pass_if_nothing_is_applicable.ids
Optional specifications may still pass if nothing is applicable
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 要件が指定されている場合、禁止仕様は無効となる

``` ids ids/invalid-prohibited_specifications_invalid_if_requirements_are_specified.ids
Prohibited specifications invalid if requirements are specified
Prohibited
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 禁止仕様は、適用可能性が一致すれば不合格となる。

``` ids ids/fail-prohibited_specifications_fails_if_the_applicability_matches.ids
Prohibited specifications fails if the applicability matches
Prohibited
IFC2X3
Entity: ''IFCWALL''
```

### 禁止仕様に該当しない場合は合格

``` ids ids/pass-prohibited_specifications_passes_if_the_applicability_does_not_matches.ids
Prohibited specifications passes if the applicability does not matches
Prohibited
IFC2X3
Entity: ''IFCWINDOW''
```

### 必要な仕様には、少なくとも1つの該当するエンティティが必要 (1/2)

``` ids ids/pass-required_specifications_need_at_least_one_applicable_entity_1_2.ids
Required specifications need at least one applicable entity (1/2)
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 必要な仕様には少なくとも1つの該当するエンティティが必要 (2/2)

``` ids ids/fail-required_specifications_need_at_least_one_applicable_entity_2_2.ids
Required specifications need at least one applicable entity (2/2)
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 仕様の任意性とファセットの任意性を組み合わせることができる

``` ids ids/pass-specification_optionality_and_facet_optionality_can_be_combined.ids
Specification optionality and facet optionality can be combined
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
Attribute: Optional,''Description'',''Foobar''
```

### 仕様のバージョンは純粋なメタデータであり、合否結果には影響しない。

``` ids ids/pass-specification_version_is_purely_metadata_and_does_not_impact_pass_or_fail_result.ids
Specification version is purely metadata and does not impact pass or fail result
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

## 材料

### データのない構成要素セットは、値チェックに失敗する

``` ids material/fail-a_constituent_set_with_no_data_will_fail_a_value_check.ids
A constituent set with no data will fail a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 素材カテゴリーは値チェックを通過する可能性がある

``` ids material/pass-a_material_category_may_pass_the_value_check.ids
A material category may pass the value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### データのない材料リストは値チェックに失敗します。

``` ids material/fail-a_material_list_with_no_data_will_fail_a_value_check.ids
A material list with no data will fail a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 材料名は値チェックを通過する可能性がある

``` ids material/pass-a_material_name_may_pass_the_value_check.ids
A material name may pass the value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 禁止ファセットは必須ファセットの反対を返す

``` ids material/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCWALL''
Requirements:
Material: Prohibited,
```

### 必須ファセットは、通常通りすべてのパラメータをチェックする。

``` ids material/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
Material: 
```

### 指定された場合、オプションの材料が渡される

``` ids material/pass-an_optional_material_passes_if_specified.ids
An optional material passes if specified
Entity: ''IFCWALL''
Requirements:
Material: Optional,''Foo''
```

### NULLの場合、オプションの素材が渡される

``` ids material/pass-an_optional_material_passes_if_null.ids
An optional material passes if null
Entity: ''IFCWALL''
Requirements:
Material: Optional,''Foo''
```

### オプションの材料は、マッチする値がなければ失敗する。

``` ids material/fail-an_optional_material_fails_if_no_value_matches.ids
An optional material fails if no value matches
Entity: ''IFCWALL''
Requirements:
Material: Optional,''Foo''
```

### 構成要素セット内のどの構成要素カテゴリーも値チェックを通過する

``` ids material/pass-any_constituent_category_in_a_constituent_set_will_pass_a_value_check.ids
Any constituent Category in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 小選挙区セット内の小選挙区名はすべて値チェックを通過する。

``` ids material/pass-any_constituent_name_in_a_constituent_set_will_pass_a_value_check.ids
Any constituent Name in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット内のどのレイヤーカテゴリーも値チェックを通過する

``` ids material/pass-any_layer_category_in_a_layer_set_will_pass_a_value_check.ids
Any layer Category in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセットに含まれるレイヤー名はすべて、値チェックを通過します。

``` ids material/pass-any_layer_name_in_a_layer_set_will_pass_a_value_check.ids
Any layer Name in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 構成要素セット内のどの材料カテゴリーも、値チェックを通過する。

``` ids material/pass-any_material_category_in_a_constituent_set_will_pass_a_value_check.ids
Any material Category in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット内のマテリアル・カテゴリーが値チェックを通過する

``` ids material/pass-any_material_category_in_a_layer_set_will_pass_a_value_check.ids
Any material Category in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### リスト内のどの材料カテゴリーも値チェックを通過する

``` ids material/pass-any_material_category_in_a_list_will_pass_a_value_check.ids
Any material Category in a list will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイル・セット内のどの材料カテゴリーも値チェックを通過します。

``` ids material/pass-any_material_category_in_a_profile_set_will_pass_a_value_check.ids
Any material category in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 構成要素セット内の材料名はすべて、値チェックを通過します。

``` ids material/pass-any_material_name_in_a_constituent_set_will_pass_a_value_check.ids
Any material Name in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセットに含まれるすべての材料名は、値チェックを通過します。

``` ids material/pass-any_material_name_in_a_layer_set_will_pass_a_value_check.ids
Any material Name in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### リスト内の材料名はすべて、値チェックを通過します。

``` ids material/pass-any_material_name_in_a_list_will_pass_a_value_check.ids
Any material Name in a list will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイル・セット内の材料名はすべて値チェックを通過します。

``` ids material/pass-any_material_name_in_a_profile_set_will_pass_a_value_check.ids
Any material Name in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイル・セット内のプロファイル・カテゴリーはすべて、値チェックを通過します。

``` ids material/pass-any_profile_category_in_a_profile_set_will_pass_a_value_check.ids
Any profile Category in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイル・セット内のプロファイル名はすべて、値チェックを通過します。

``` ids material/pass-any_profile_name_in_a_profile_set_will_pass_a_value_check.ids
Any profile Name in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 任意の素材を持つ要素は、空の素材ファセットを渡します。

``` ids material/pass-elements_with_any_material_will_pass_an_empty_material_facet.ids
Elements with any material will pass an empty material facet
Entity: ''IFCWALL''
Requirements:
Material: 
```

### 素材のない要素は常に失敗する

``` ids material/fail-elements_without_a_material_always_fail.ids
Elements without a material always fail
Entity: ''IFCWALL''
Requirements:
Material: 
```

### データのない材料は値チェックに失敗する

``` ids material/fail-material_with_no_data_will_fail_a_value_check.ids
Material with no data will fail a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### オカレンスは、そのタイプからマテリアルを継承することができます。

``` ids material/pass-occurrences_can_inherit_materials_from_their_types.ids
Occurrences can inherit materials from their types
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### オカレンスは、そのタイプからマテリアルを上書きすることができます。

``` ids material/pass-occurrences_can_override_materials_from_their_types.ids
Occurrences can override materials from their types
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット名は値チェックを通過する

``` ids material/pass-a_layer_set_name_will_pass_a_value_check.ids
A layer set name will pass the value check
Entity: ''IFCWALL''
Requirements:
Material: ''Bar''
```

## 一部

### グループ・エンティティは、正確に1/2に一致しなければならない。

``` ids partof/fail-a_group_entity_must_match_exactly_1_2.ids
A group entity must match exactly 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCGROUP'',IFCRELASSIGNSTOGROUP
```

### グループ・エンティティは、正確に2/2に一致しなければならない

``` ids partof/pass-a_group_entity_must_match_exactly_2_2.ids
A group entity must match exactly 2/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCINVENTORY'',IFCRELASSIGNSTOGROUP
```

### グループの定義済みタイプは、正確に 1/2 に一致しなければならない。

``` ids partof/invalid-a_group_predefined_type_must_match_exactly_1_2.ids
A group predefined type must match exactly 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCINVENTORY'',''BUNNARY'',IFCRELASSIGNSTOGROUP
```

### グループの定義済みタイプは、2/2 に正確に一致しなければならない。

``` ids partof/pass-a_group_predefined_type_must_match_exactly_2_2.ids
A group predefined type must match exactly 2/2
IFC4
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCINVENTORY'',''BUNNY'',IFCRELASSIGNSTOGROUP
```

### グループ化された要素はグループ関係を渡す

``` ids partof/pass-a_grouped_element_passes_a_group_relationship.ids
A grouped element passes a group relationship
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELASSIGNSTOGROUP
```

### 非集約要素は集約関係に失敗する

``` ids partof/fail-a_non_aggregated_element_fails_an_aggregate_relationship.ids
A non aggregated element fails an aggregate relationship
Entity: ''IFCWALL''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### グループ化されていない要素はグループ関係に失敗する

``` ids partof/fail-a_non_grouped_element_fails_a_group_relationship.ids
A non grouped element fails a group relationship
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELASSIGNSTOGROUP
```

### 禁止ファセットは必須ファセットの反対を返す

``` ids partof/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCWALL''
Requirements:
PartOf: Prohibited,Pattern(''.*''),IFCRELAGGREGATES
```

### 必須ファセットは、通常通りすべてのパラメータをチェックする。

``` ids partof/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### 集合体は、祖先全体をパスすることができる。

``` ids partof/pass-an_aggregate_entity_may_pass_any_ancestral_whole_passes.ids
An aggregate entity may pass any ancestral whole passes
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCELEMENTASSEMBLY'',IFCRELAGGREGATES
```

### 集合体は、1/2全体の実体を指定することができる。

``` ids partof/pass-an_aggregate_may_specify_the_entity_of_the_whole_1_2.ids
An aggregate may specify the entity of the whole 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSLAB'',IFCRELAGGREGATES
```

### 集合体は、全体の実体を指定することができる 2/2

``` ids partof/fail-an_aggregate_may_specify_the_entity_of_the_whole_2_2.ids
An aggregate may specify the entity of the whole 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCWALL'',IFCRELAGGREGATES
```

### 集合体は、1/2全体の定義済みの型を指定することができる。

``` ids partof/pass-an_aggregate_may_specify_the_predefined_type_of_the_whole_1_2.ids
An aggregate may specify the predefined type of the whole 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSLAB'',''BASESLAB'',IFCRELAGGREGATES
```

### 集合体は、2/2全体の定義済みのタイプを指定することができる。

``` ids partof/fail-an_aggregate_may_specify_the_predefined_type_of_the_whole_2_2.ids
An aggregate may specify the predefined type of the whole 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSLAB'',''SLABRADOR'',IFCRELAGGREGATES
```

### 含まれる要素はすべて、包含関係 1/2 を通過する。

``` ids partof/fail-any_contained_element_passes_a_containment_relationship_1_2.ids
Any contained element passes a containment relationship 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### 含まれる要素はすべて包含関係をパスする 2/2

``` ids partof/pass-any_contained_element_passes_a_containment_relationship_2_2.ids
Any contained element passes a containment relationship 2/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### ネストされた部分はすべてネスト関係をパスする

``` ids partof/pass-any_nested_part_passes_a_nest_relationship.ids
Any nested part passes a nest relationship
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: Pattern(''.*''),IFCRELNESTS
```

### ネストされた全体はネスト関係に失敗する

``` ids partof/fail-any_nested_whole_fails_a_nest_relationship.ids
Any nested whole fails a nest relationship
IFC4
Entity: ''IFCFURNITURE''
Requirements:
PartOf: Pattern(''.*''),IFCRELNESTS
```

### 巣作りは間接的かもしれない

``` ids partof/pass-nesting_may_be_indirect.ids
Nesting may be indirect
IFC4
Entity: ''IFCMECHANICALFASTENER''
Requirements:
PartOf: ''IFCFURNITURE'',IFCRELNESTS
```

### 集約された部分は、集約された関係を渡す

``` ids partof/pass-the_aggregated_part_passes_an_aggregate_relationship.ids
The aggregated part passes an aggregate relationship
Entity: ''IFCWALL''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### 集約された全体は集約関係に失敗する

``` ids partof/fail-the_aggregated_whole_fails_an_aggregate_relationship.ids
The aggregated whole fails an aggregate relationship
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### コンテナ・エンティティは、1/2

``` ids partof/fail-the_container_entity_must_match_exactly_1_2.ids
The container entity must match exactly 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSITE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナの実体は、2/2 に正確に一致しなければならない。

``` ids partof/pass-the_container_entity_must_match_exactly_2_2.ids
The container entity must match exactly 2/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSPACE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナ自体が常に失敗する

``` ids partof/fail-the_container_itself_always_fails.ids
The container itself always fails
Entity: ''IFCSPACE''
Requirements:
PartOf: Pattern(''.*''),IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナは、指定されたリレーション1/2を使用して関連付けられなければならない。

``` ids partof/pass-the_container_must_be_related_using_specified_relation_1_2.ids
The container must be related using specified relation 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSPACE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナは、指定された2/2の関係を使って関連づけられなければならない。

``` ids partof/fail-the_container_must_be_related_using_specified_relation_2_2.ids
The container must be related using specified relation 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSPACE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### 封じ込めは間接的な1/2

``` ids partof/pass-the_containment_can_be_indirect_1_2.ids
The containment can be indirect 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCBUILDING'',IFCRELAGGREGATES
```

### 封じ込めは間接的な2/2

``` ids partof/fail-the_containment_can_be_indirect_2_2.ids
The containment can be indirect 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCBUILDING'',IFCRELAGGREGATES
```

### コンテナの定義済みタイプは、1/2 に正確に一致する必要があります。

``` ids partof/fail-the_container_predefined_type_must_match_exactly_1_2.ids
The container predefined type must match exactly 1/2
IFC4
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSPACE'',''WARREN'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナの定義済みタイプは、2/2 に正確に一致する必要があります。

``` ids partof/pass-the_container_predefined_type_must_match_exactly_2_2.ids
The container predefined type must match exactly 2/2
IFC4
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSPACE'',''BURROW'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### ネスト・エンティティは、正確に1/2に一致しなければならない。

``` ids partof/fail-the_nest_entity_must_match_exactly_1_2.ids
The nest entity must match exactly 1/2
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCBEAM'',IFCRELNESTS
```

### ネスト・エンティティは2/2に正確に一致しなければならない

``` ids partof/pass-the_nest_entity_must_match_exactly_2_2.ids
The nest entity must match exactly 2/2
IFC4
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCFURNITURE'',IFCRELNESTS
```

### ネストの定義済み型は、1/2 に正確に一致しなければならない。

``` ids partof/fail-the_nest_predefined_type_must_match_exactly_1_2.ids
The nest predefined type must match exactly 1/2
IFC4
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCFURNITURE'',''LITTERBOX'',IFCRELNESTS
```

### ネストの定義済みタイプは、2/2 に正確に一致しなければならない。

``` ids partof/pass-the_nest_predefined_type_must_match_exactly_2_2.ids
The nest predefined type must match exactly 2/2
IFC4
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCFURNITURE'',''WATERBOTTLE'',IFCRELNESTS
```

## プロパティ

### 論理的な未知数は一致しないとみなされ、パスしない。

IFCDURATION は IFC2x3 では使用できません。

``` ids property/fail-a_logical_unknown_is_considered_false_and_will_not_pass.ids
A logical unknown is considered as not matching and will not pass
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLOGICAL
```

### 名前チェックは、任意の文字列値を持つプロパティにマッチします。

``` ids property/pass-a_name_check_will_match_any_property_with_any_string_value.ids
A name check will match any property with any string value
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 名前チェックは、任意の量と任意の値をマッチさせます。

``` ids property/pass-a_name_check_will_match_any_quantity_with_any_value.ids
A name check will match any quantity with any value
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE
```

### 文字列として指定された数値は、文字列として扱われる。

``` ids property/pass-a_number_specified_as_a_string_is_treated_as_a_string.ids
A number specified as a string is treated as a string
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''1''
```

### 禁止ファセットは必須ファセットの反対を返す

``` ids property/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCWALL''
Requirements:
Property: Prohibited,''Foo_Bar'',''Foo''
```

### falseに設定されたプロパティは、依然として値とみなされ、名前チェックを通過する。

``` ids property/pass-a_property_set_to_false_is_still_considered_a_value_and_will_pass_a_name_check.ids
A property set to false is still considered a value and will pass a name check
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN
```

### trueに設定されたプロパティは、名前チェックをパスする。

``` ids property/pass-a_property_set_to_true_will_pass_a_name_check.ids
A property set to true will pass a name check
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN
```

### 必須ファセットは、通常通りすべてのパラメータをチェックする。

``` ids property/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 持続時間がゼロであれば合格

IFCDURATION は IFC2x3 では使用できません。

``` ids property/pass-a_zero_duration_will_pass.ids
A zero duration will pass
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDURATION
```

### すべてのマッチング・プロパティは、1/3の要件を満たさなければならない。

``` ids property/pass-all_matching_properties_must_satisfy_requirements_1_3.ids
All matching properties must satisfy requirements 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,''x''
```

### すべてのマッチング物件は、2/3の要件を満たさなければならない。

``` ids property/pass-all_matching_properties_must_satisfy_requirements_2_3.ids
All matching properties must satisfy requirements 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,''x''
```

### すべてのマッチング物件は、3/3の要件を満たさなければならない。

``` ids property/fail-all_matching_properties_must_satisfy_requirements_3_3.ids
All matching properties must satisfy requirements 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,''x''
```

### 一致するすべてのプロパティセットは、要件 1/3 を満たさなければならない。

``` ids property/pass-all_matching_property_sets_must_satisfy_requirements_1_3.ids
All matching property sets must satisfy requirements 1/3
Entity: ''IFCWALL''
Requirements:
Property: Pattern(''Foo_.*''),''Foo'',IFCLABEL
```

### すべてのマッチング・プロパティ・セットは、2/3の要件を満たさなければならない。

``` ids property/fail-all_matching_property_sets_must_satisfy_requirements_2_3.ids
All matching property sets must satisfy requirements 2/3
Entity: ''IFCWALL''
Requirements:
Property: Pattern(''Foo_.*''),''Foo'',IFCLABEL
```

### 一致するすべてのプロパティセットは、要件 3/3 を満たさなければならない。

``` ids property/pass-all_matching_property_sets_must_satisfy_requirements_3_3.ids
All matching property sets must satisfy requirements 3/3
Entity: ''IFCWALL''
Requirements:
Property: Pattern(''Foo_.*''),''Foo'',IFCLABEL
```

### 空の文字列はマッチしないとみなされ、通過しません。

``` ids property/fail-an_empty_string_is_considered_false_and_will_not_pass.ids
An empty string is considered not matching and will not pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### オプションのファセットは、1/2の結果にかかわらず常にパスする。

``` ids property/pass-an_optional_facet_always_passes_regardless_of_outcome_1_2.ids
An optional facet always passes regardless of outcome 1/2
Entity: ''IFCWALL''
Requirements:
Property: Optional,''Foo_Bar'',''Foo'',IFCLABEL
```

### オプションのファセットは、結果にかかわらず常にパスする 2/2

``` ids property/pass-an_optional_facet_always_passes_regardless_of_outcome_2_2.ids
An optional facet always passes regardless of outcome 2/2
Entity: ''IFCWALL''
Requirements:
Property: Optional,''Foo_Bar'',''Bar'',IFCLABEL
```

### バウンデッド・プロパティで一致する値はすべて、1/4 を通過します。

``` ids property/pass-any_matching_value_in_a_bounded_property_will_pass_1_4.ids
Any matching value in a bounded property will pass 1/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''1''
```

### バウンデッド・プロパティで一致する値はすべて2/4をパスする。

``` ids property/pass-any_matching_value_in_a_bounded_property_will_pass_2_4.ids
Any matching value in a bounded property will pass 2/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''5''
```

### バウンデッド・プロパティで一致する値はすべて、3/4 を通過する。

``` ids property/pass-any_matching_value_in_a_bounded_property_will_pass_3_4.ids
Any matching value in a bounded property will pass 3/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''3''
```

### バウンデッド・プロパティで一致する値はすべてパスする。

``` ids property/fail-any_matching_value_in_a_bounded_property_will_pass_4_4.ids
Any matching value in a bounded property will pass 4/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''2''
```

### リスト・プロパティで一致する値があれば、1/3 を通過します。

``` ids property/pass-any_matching_value_in_a_list_property_will_pass_1_3.ids
Any matching value in a list property will pass 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''X''
```

### リスト・プロパティ内の一致する値はすべて、2/3 を通過する。

``` ids property/pass-any_matching_value_in_a_list_property_will_pass_2_3.ids
Any matching value in a list property will pass 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Y''
```

### リスト・プロパティ内の一致する値はすべてパスする。

``` ids property/fail-any_matching_value_in_a_list_property_will_pass_3_3.ids
Any matching value in a list property will pass 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Z''
```

### テーブルのプロパティに一致する値があれば、1/3 を通過します。

``` ids property/pass-any_matching_value_in_a_table_property_will_pass_1_3.ids
Any matching value in a table property will pass 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''X''
```

### テーブルのプロパティに一致する値があれば、2/3を通過する。

``` ids property/pass-any_matching_value_in_a_table_property_will_pass_2_3.ids
Any matching value in a table property will pass 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''1''
```

### テーブルのプロパティに一致する値があれば、3/3をパスする。

``` ids property/fail-any_matching_value_in_a_table_property_will_pass_3_3.ids
Any matching value in a table property will pass 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Y''
```

### 列挙されたプロパティに一致する値があれば、1/3 を通過します。

``` ids property/pass-any_matching_value_in_an_enumerated_property_will_pass_1_3.ids
Any matching value in an enumerated property will pass 1/3
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Pset_WallCommon'',''Status'',IFCLABEL,''EXISTING''
```

### 列挙されたプロパティに一致する値があれば、2/3 を通過します。

``` ids property/pass-any_matching_value_in_an_enumerated_property_will_pass_2_3.ids
Any matching value in an enumerated property will pass 2/3
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Pset_WallCommon'',''Status'',IFCLABEL,''DEMOLISH''
```

### 列挙されたプロパティに一致する値がない場合、失敗します。

``` ids property/fail-no_matching_value_in_an_enumerated_property_will_fail_3_3.ids
No matching value in an enumerated property will fail 3/3
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Pset_WallCommon'',''Status'',IFCLABEL,''NEW''
```

### ブール値は小文字の文字列で指定する必要があります。

``` ids property/fail-booleans_must_be_specified_as_lowercase_strings_1_3.ids
Booleans must be specified as lowercase strings 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN,''true''
```

### ブーリアンは小文字の文字列として指定しなければならない。

``` ids property/pass-booleans_must_be_specified_as_lowercase_strings_2_3.ids
Booleans must be specified as lowercase strings 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN,''false''
```

### ブーリアンは小文字の文字列として指定しなければならない。

``` ids property/invalid-booleans_must_be_specified_as_lowercase_strings_3_3.ids
Booleans must be specified as lowercase strings 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN,''FALSE''
```

### 複雑なプロパティはサポートされていません。

``` ids property/fail-complex_properties_are_not_supported_1_2.ids
Complex properties are not supported 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE
```

### 複雑なプロパティはサポートされていません 2/2

``` ids property/fail-complex_properties_are_not_supported_2_2.ids
Complex properties are not supported 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo'',''MyLength'',IFCLENGTHMEASURE
```

### 日付は文字列として扱われる 1/2

``` ids property/pass-dates_are_treated_as_strings_1_2.ids
Dates are treated as strings 1/2
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDATE,''2022-01-01''
```

### 日付は文字列として扱われる 2/2

``` ids property/fail-dates_are_treated_as_strings_2_2.ids
Dates are treated as strings 2/2
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDATE,''2022-01-01''
```

### 持続時間は文字列として扱われる 1/2

IFCDURATION は IFC2x3 では使用できません。

``` ids property/fail-durations_are_treated_as_strings_1_2.ids
Durations are treated as strings 1/2
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDURATION,''PT16H''
```

### デュレーションはストリングス2/2として扱われる

IFCDURATION は IFC2x3 では使用できません。

``` ids property/pass-durations_are_treated_as_strings_2_2.ids
Durations are treated as strings 2/2
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDURATION,''PT16H''
```

### 一致するpsetを持つがプロパティを持たない要素も失敗する。

``` ids property/fail-elements_with_a_matching_pset_but_no_property_also_fail.ids
Elements with a matching pset but no property also fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### プロパティを持たない要素は常に失敗する

``` ids property/fail-elements_with_no_properties_always_fail.ids
Elements with no properties always fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### IDSは識別子のような文字列の切り捨てを扱わない

``` ids property/fail-ids_does_not_handle_string_truncation_such_as_for_identifiers.ids
IDS does not handle string truncation such as for identifiers
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCIDENTIFIER,''123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345_extra_characters''
```

### 複数のプロパティが一致する場合、すべての値が要件 1/2 を満たさなければならない。

``` ids property/pass-if_multiple_properties_are_matched__all_values_must_satisfy_requirements_1_2.ids
If multiple properties are matched, all values must satisfy requirements 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,Enumeration(''x'',''y'')
```

### 複数のプロパティが一致する場合、すべての値が要件 2/2 を満たさなければならない。

``` ids property/fail-if_multiple_properties_are_matched__all_values_must_satisfy_requirements_2_2.ids
If multiple properties are matched, all values must satisfy requirements 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,Enumeration(''x'',''y'')
```

### 整数値は型キャストを使用してチェックされる 1/4

``` ids property/pass-integer_values_are_checked_using_type_casting_1_4.ids
Integer values are checked using type casting 1/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42''
```

### 整数値を10進数2/4で保存することはできません。

``` ids property/invalid-integer_values_cannot_be_stored_with_decimal_2_4.ids
Integer values cannot be stored with decimal 2/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42.''
```

### 整数値を10進数3/4で保存することはできません。

``` ids property/invalid-integer_values_cannot_be_stored_with_decimal_3_4.ids
Integer values cannot be stored with decimal 3/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42.0''
```

### 整数値は型キャストを使ってチェックされる 4/4

``` ids property/invalid-integer_values_are_checked_using_type_casting_4_4.ids
Integer values are checked using type casting 4/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42.3''
```

### メジャーは、IFC データ型 1/2 を指定するために使用されます。

``` ids property/fail-measures_are_used_to_specify_an_ifc_data_type_1_2.ids
Measures are used to specify an IFC data type 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCTIMEMEASURE,''2''
```

### メジャーは、IFC データ型を指定するために使用されます。

``` ids property/pass-measures_are_used_to_specify_an_ifc_data_type_2_2.ids
Measures are used to specify an IFC data type 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCTIMEMEASURE,''2''
```

### 非アスキー文字はエンコードなしで扱われる

``` ids property/pass-non_ascii_characters_are_treated_without_encoding.ids
Non-ascii characters are treated without encoding
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''♫Don'tÄrgerhôtelЊет''
```

### 特別にフォーマットされた数字だけが許される 1/4

``` ids property/invalid-only_specifically_formatted_numbers_are_allowed_1_4.ids
Only specifically formatted numbers are allowed 1/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42,3''
```

### 特別にフォーマットされた数字のみが許される 2/4

``` ids property/invalid-only_specifically_formatted_numbers_are_allowed_2_4.ids
Only specifically formatted numbers are allowed 2/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''123,4.5''
```

### 特別にフォーマットされた数字だけが許される 3/4

``` ids property/pass-only_specifically_formatted_numbers_are_allowed_3_4.ids
Only specifically formatted numbers are allowed 3/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.2345e3''
```

### 特別にフォーマットされた数字のみが許される 4/4

``` ids property/pass-only_specifically_formatted_numbers_are_allowed_4_4.ids
Only specifically formatted numbers are allowed 4/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.2345E3''
```

### 定義済みプロパティはサポートされていますが、推奨されません。

``` ids property/pass-predefined_properties_are_supported_but_discouraged_1_2.ids
Predefined properties are supported but discouraged 1/2
Entity: ''IFCDOOR''
Requirements:
Property: ''Foo_Bar'',''PanelOperation'',IFCDOORPANELOPERATIONENUM,''SWINGING''
```

### 定義済みプロパティはサポートされるが、推奨されない 2/2

``` ids property/fail-predefined_properties_are_supported_but_discouraged_2_2.ids
Predefined properties are supported but discouraged 2/2
Entity: ''IFCDOOR''
Requirements:
Property: ''Foo_Bar'',''PanelOperation'',IFCDOORPANELOPERATIONENUM,''SWONGING''
```

### プロパティは型から継承できる 1/2

``` ids property/pass-properties_can_be_inherited_from_the_type_1_2.ids
Properties can be inherited from the type 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### プロパティは2/2型から継承できる。

``` ids property/pass-properties_can_be_inherited_from_the_type_2_2.ids
Properties can be inherited from the type 2/2
Entity: ''IFCWALLTYPE''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### プロパティは、オカレンスによってオーバーライドすることができます 1/2

``` ids property/pass-properties_can_be_overriden_by_an_occurrence_1_2.ids
Properties can be overriden by an occurrence 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### プロパティはオカレンスによってオーバーライドできる 2/2

``` ids property/fail-properties_can_be_overriden_by_an_occurrence_2_2.ids
Properties can be overriden by an occurrence 2/2
Entity: ''IFCWALLTYPE''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### NULL値を持つプロパティは失敗する

``` ids property/fail-properties_with_a_null_value_fail.ids
Properties with a null value fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 数量も適切な尺度と一致しなければならない。

``` ids property/fail-quantities_must_also_match_the_appropriate_measure.ids
Quantities must also match the appropriate measure
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCAREAMEASURE
```

### 実数値は、型キャスト1/3を使ってチェックされる。

``` ids property/pass-real_values_are_checked_using_type_casting_1_3.ids
Real values are checked using type casting 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42''
```

### 実数値は型キャスト2/3を使ってチェックされる。

``` ids property/pass-real_values_are_checked_using_type_casting_2_3.ids
Real values are checked using type casting 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42.0''
```

### 実数値は型キャストでチェックされる 3/3

``` ids property/pass-real_values_are_checked_using_type_casting_3_3.ids
Real values are checked using type casting 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42.3''
```

### 参照プロパティはオブジェクトとして扱われ、サポートされない

``` ids property/fail-reference_properties_are_treated_as_objects_and_not_supported.ids
Reference properties are treated as objects and not supported
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 異なる値に対して値を指定しても失敗する

``` ids property/fail-specifying_a_value_fails_against_different_values.ids
Specifying a value fails against different values
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 値を指定すると、大文字と小文字を区別してマッチを行う 1/2

``` ids property/pass-specifying_a_value_performs_a_case_sensitive_match_1_2.ids
Specifying a value performs a case-sensitive match 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 値を指定すると、大文字と小文字を区別してマッチする 2/2

``` ids property/fail-specifying_a_value_performs_a_case_sensitive_match_2_2.ids
Specifying a value performs a case-sensitive match 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 単位変換は、IDS 指定の標準単位 1/2 に行うものとする。

``` ids property/fail-unit_conversions_shall_take_place_to_ids_nominated_standard_units_1_2.ids
Unit conversions shall take place to IDS-nominated standard units 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''2''
```

### 単位変換は、IDS 指定の標準単位 2/2 に行うものとする。

``` ids property/pass-unit_conversions_shall_take_place_to_ids_nominated_standard_units_2_2.ids
Unit conversions shall take place to IDS-nominated standard units 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''2''
```

### プロパティは、関連するオブジェクト・タイプに関連付けることができる。

監査ツールは、予約接頭辞`Pset_`を適切なオブジェクトに変換する、
but they can also be associated to the relevant types. E.g. `Pset_WallCommon` on `IFCWALLTYPE`.

プロパティセットの1つが無効な値を定義しているため、提供されたIFCは失敗します。`FOOBAR`.

``` ids property/fail-properties_can_be_associated_to_relevant_object_types.ids
Properties can be associated to relevant object types
Optional
IFC4
Entity: ''IFCWALLTYPE''
Requirements:
Property: ''Pset_WallCommon'',''FireRating'',IFCLABEL,Pattern(''(-|[0-9]{2,3})\/(-|[0-9]{2,3})\/(-|[0-9]{2,3})'')
```

## 制限

### バウンドは排他的であることができる 1/3

``` ids restriction/fail-a_bound_can_be_exclusive_1_3.ids
A bound can be exclusive 1/3
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinExclusive(''0'') MaxExclusive(''10'')
```

### バウンドは1/4を含むことができる。

``` ids restriction/pass-a_bound_can_be_inclusive_1_4.ids
A bound can be inclusive 1/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### バウンドは排他的であることができる2/3

``` ids restriction/pass-a_bound_can_be_exclusive_2_3.ids
A bound can be exclusive 2/3
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinExclusive(''0'') MaxExclusive(''10'')
```

### バウンドは包括的な2/4

``` ids restriction/pass-a_bound_can_be_inclusive_2_4.ids
A bound can be inclusive 2/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### バウンドは排他的である。

``` ids restriction/fail-a_bound_can_be_exclusive_3_3.ids
A bound can be exclusive 3/3
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinExclusive(''0'') MaxExclusive(''10'')
```

### 境界は3/4を含むことができる。

``` ids restriction/pass-a_bound_can_be_inclusive_3_4.ids
A bound can be inclusive 3/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### バウンドは4/4を含むことができる

``` ids restriction/fail-a_bound_can_be_inclusive_4_4.ids
A bound can be inclusive 4/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### 列挙は大文字と小文字を区別してマッチする 1/3

``` ids restriction/pass-an_enumeration_matches_case_sensitively_1_3.ids
An enumeration matches case sensitively 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 列挙は大文字と小文字を区別してマッチする 2/3

``` ids restriction/pass-an_enumeration_matches_case_sensitively_2_3.ids
An enumeration matches case sensitively 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 列挙は大文字と小文字を区別してマッチする 3/3

``` ids restriction/fail-an_enumeration_matches_case_sensitively_3_3.ids
An enumeration matches case sensitively 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 列挙は大文字と小文字を区別してマッチする 4/3

``` ids restriction/fail-an_enumeration_matches_case_sensitively_4_3.ids
An enumeration matches case sensitively 4/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 長さチェックは1/2

``` ids restriction/fail-length_checks_can_be_used_1_2.ids
Length checks can be used 1/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Length(''2'')
```

### 長さチェックは2/2

``` ids restriction/pass-length_checks_can_be_used_2_2.ids
Length checks can be used 2/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Length(''2'')
```

### 最大と最小の長さチェックが可能 1/3

``` ids restriction/fail-max_and_min_length_checks_can_be_used_1_3.ids
Max and min length checks can be used 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### 最大と最小の長さチェックが可能 2/3

``` ids restriction/pass-max_and_min_length_checks_can_be_used_2_3.ids
Max and min length checks can be used 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### 最大と最小の長さのチェックが可能 3/3

``` ids restriction/pass-max_and_min_length_checks_can_be_used_3_3.ids
Max and min length checks can be used 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### 最大と最小の長さのチェックが可能 4/3

``` ids restriction/fail-max_and_min_length_checks_can_be_used_4_3.ids
Max and min length checks can be used 4/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### どの番号でもパターンは常に無効

``` ids restriction/invalid-patterns_always_fail_on_any_number.ids
Patterns always invalid on any number
Optional
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',Pattern(''.*'')
```

### パターンはストリングスにのみ機能し、それ以外には機能しない

``` ids restriction/invalid-patterns_only_work_on_strings_and_nothing_else.ids
Patterns only work on strings and nothing else
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',Pattern(''.*'')
```

### Regex パターンが使える 1/3

``` ids restriction/pass-regex_patterns_can_be_used_1_3.ids
Regex patterns can be used 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンは2/3

``` ids restriction/pass-regex_patterns_can_be_used_2_3.ids
Regex patterns can be used 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンは3/3で使用可能

``` ids restriction/fail-regex_patterns_can_be_used_3_3.ids
Regex patterns can be used 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンは OR 1/3 で機能する

``` ids restriction/pass-regex_patterns_work_in_OR_1_3.ids
Regex patterns work in OR 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'') Pattern(''[a-z]{2}[0-9]{2}'')
```

### 正規表現パターンはOR 2/3で機能する

``` ids restriction/pass-regex_patterns_work_in_OR_2_3.ids
Regex patterns work in OR 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[a-z]{2}[0-9]{2}'') Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンはOR 3/3で機能する

``` ids restriction/fail-regex_patterns_work_in_OR_3_3.ids
Regex patterns work in OR 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[a-z]{3}[0-9]{2}'') Pattern(''[A-Z]{3}[0-9]{2}'')
```

## 寛容

### 浮動小数点正数の下界パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_high_number_lower_bound.ids
Comparison tolerance for floating point positive high number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点正数の下限が失敗した場合の比較許容度

``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_high_number_lower_bound.ids
Comparison tolerance for floating point positive high number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点正数の上限パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_high_number_upper_bound.ids
Comparison tolerance for floating point positive high number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点正数の上限失敗の比較許容度

``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_high_number_upper_bound.ids
Comparison tolerance for floating point positive high number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点数の下限が1つ失敗した場合の比較許容誤差

``` ids tolerance/fail-comparison_tolerance_for_floating_point_one_lower_bound.ids
Comparison tolerance for floating point one lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点1下界パスの比較許容差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_one_lower_bound.ids
Comparison tolerance for floating point one lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点1上限パスの比較許容差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_one_upper_bound.ids
Comparison tolerance for floating point one upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点数の1つの上限が失敗した場合の比較許容誤差

``` ids tolerance/fail-comparison_tolerance_for_floating_point_one_upper_bound.ids
Comparison tolerance for floating point one upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点正の少数点下界不合格時の比較許容誤差

``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_low_number_lower_bound.ids
Comparison tolerance for floating point positive low number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点正数下界パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_low_number_lower_bound.ids
Comparison tolerance for floating point positive low number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点正の少数点上限パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_low_number_upper_bound.ids
Comparison tolerance for floating point positive low number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点正の少数点上限失敗の比較許容誤差

``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_low_number_upper_bound.ids
Comparison tolerance for floating point positive low number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点ゼロ下限失敗の比較許容範囲

``` ids tolerance/fail-comparison_tolerance_for_floating_point_zero_lower_bound.ids
Comparison tolerance for floating point zero lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点ゼロ下限パスの比較許容差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_zero_lower_bound.ids
Comparison tolerance for floating point zero lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点ゼロ上限パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_zero_upper_bound.ids
Comparison tolerance for floating point zero upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点ゼロ上限失敗の比較許容範囲

``` ids tolerance/fail-comparison_tolerance_for_floating_point_zero_upper_bound.ids
Comparison tolerance for floating point zero upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点負数下限失敗の比較許容範囲

``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_low_number_lower_bound.ids
Comparison tolerance for floating point negative low number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負数下界パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_low_number_lower_bound.ids
Comparison tolerance for floating point negative low number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負の少数点上限パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_low_number_upper_bound.ids
Comparison tolerance for floating point negative low number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負数の上限失敗の比較許容範囲

``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_low_number_upper_bound.ids
Comparison tolerance for floating point negative low number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負の1下限が失敗した場合の比較許容誤差

``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_one_lower_bound.ids
Comparison tolerance for floating point negative one lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点負の1下界パスの比較許容差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_one_lower_bound.ids
Comparison tolerance for floating point negative one lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点負の1上限パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_one_upper_bound.ids
Comparison tolerance for floating point negative one upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点負1上限失敗の比較許容誤差

``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_one_upper_bound.ids
Comparison tolerance for floating point negative one upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点負の高数値の下限が失敗した場合の比較許容度

``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_high_number_lower_bound.ids
Comparison tolerance for floating point negative high number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### 浮動小数点負の高数値下界パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_high_number_lower_bound.ids
Comparison tolerance for floating point negative high number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### 浮動小数点負の高数値上限パスの比較許容誤差

``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_high_number_upper_bound.ids
Comparison tolerance for floating point negative high number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### 浮動小数点負の高数値上限失敗の比較許容範囲

``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_high_number_upper_bound.ids
Comparison tolerance for floating point negative high number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### ゼロより大きい浮動小数点レンジの比較許容誤差は排他的失敗となる

``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_greater_than_zero_exclusive.ids
Comparison tolerance for floating point range greater than zero exclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinExclusive(''0.'')
```

### ゼロより大きい浮動小数点レンジの比較許容差 排他的パス

``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_greater_than_zero_exclusive.ids
Comparison tolerance for floating point range greater than zero exclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinExclusive(''0.'')
```

### ゼロより大きい浮動小数点レンジの比較許容誤差は失敗する。

``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_greater_than_zero_inclusive.ids
Comparison tolerance for floating point range greater than zero inclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinInclusive(''0.'')
```

### ゼロより大きい浮動小数点レンジの比較許容誤差。

``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_greater_than_zero_inclusive.ids
Comparison tolerance for floating point range greater than zero inclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinInclusive(''0.'')
```

### ゼロより小さい浮動小数点レンジの比較許容誤差は排他的に失敗する。

``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_lower_than_zero_exclusive.ids
Comparison tolerance for floating point range lower than zero exclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxExclusive(''0.'')
```

### ゼロより低い浮動小数点レンジの比較許容差 排他的パス

``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_lower_than_zero_exclusive.ids
Comparison tolerance for floating point range lower than zero exclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxExclusive(''0.'')
```

### ゼロより小さい浮動小数点レンジの比較許容誤差は失敗する。

``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_lower_than_zero_inclusive.ids
Comparison tolerance for floating point range lower than zero inclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxInclusive(''0.'')
```

### 浮動小数点の範囲がゼロより小さい場合の比較許容誤差。

``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_lower_than_zero_inclusive.ids
Comparison tolerance for floating point range lower than zero inclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxInclusive(''0.'')
```
