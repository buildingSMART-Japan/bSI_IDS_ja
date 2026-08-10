# ドキュメントのテストケース
このドキュメントは、テストケースの自動生成を支援するものです。

有効なIDSの実装はすべて、提供されたテストケースの期待値に対して同一の挙動を示す必要があります。

これらは、IFC検証の期待される挙動を記述するために設計されており、期待される実装における曖昧さを排除するため、すべての標準的なケースおよびエッジケースを網羅している必要があります。

テストケースは、テーマ（属性、エンティティなど）ごとにフォルダに整理され、対応するIFC/IDS ペアの検証結果に応じて、3つのグループ（合格、不合格、無効）に分類されます。

| ファイル名の接頭辞 | 説明 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| pass- | すべての要件が満たされている |
| fail- | 少なくとも1つの要件を満たしていない |
| invalid- | 少なくとも1つの要件を満たしていない（無効なファイルは監査ツールの要件に準拠しておらず、IFCの内容にかかわらず、これらの要件を満たすことはできなかった） |

IDSファイルは、リポジトリ内の`CreateTestCases`ターゲットを実行するこのスクリプトのデータから生成されます。

IFCファイルは、[IfcOpenShellリポジトリ](https://blenderbim.org/docs-python/ifctester.html)で以前に行われた作業からインポートされ、必要に応じて修正が加えられました。

## 属性
### 禁止ファセットは、必須ファセットとは逆の結果を返します
``` ids attribute/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
IFC2X3 IFC4 IFC4X3_ADD2
Entity: ''IFCWALL''
Requirements:
Attribute: Prohibited,''Name''
```

### 必須のファセットは、通常通りすべてのパラメータをチェックします
``` ids attribute/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### オプションの属性は、指定された場合に有効となります
``` ids attribute/pass-an_optional_attribute_passes_if_specified.ids
An optional attribute passes if specified
Entity: ''IFCWALL''
Requirements:
Attribute: Optional,''Name'', ''Foobar''
```

### オプションの属性は、nullの場合に通過する
``` ids attribute/pass-an_optional_attribute_passes_if_null.ids
An optional attribute passes if null
Entity: ''IFCWALL''
Requirements:
Attribute: Optional,''Name'', ''Foobar''
```

### オプションの属性は、空の場合、失敗となります
``` ids attribute/fail-an_optional_attribute_fails_if_empty.ids
An optional attribute fails if empty
Entity: ''IFCWALL''
Requirements:
Attribute: Optional,''Name'', ''Foobar''
```

### 属性はインスタンスには継承されません
``` ids attribute/fail-attributes_are_not_inherited_by_the_occurrence.ids
Attributes are not inherited by the occurrence
Entity: ''IFCWALL''
Requirements:
Attribute: ''Description'',''Foobar''
```

### オブジェクトを参照する属性は、
``` ids attribute/pass-attributes_referencing_an_object_should_pass.ids
Attributes referencing an object should pass
IFC4
Entity: ''IFCTASK''
Requirements:
Attribute: ''TaskTime''
```

### 属性では、文字列の大文字と小文字を区別してチェックすべきである 1/2
``` ids attribute/pass-attributes_should_check_strings_case_sensitively_1_2.ids
Attributes should check strings case sensitively 1/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Foobar''
```

### 属性では、文字列の大文字と小文字を区別してチェックすべきである 2/2
``` ids attribute/fail-attributes_should_check_strings_case_sensitively_2_2.ids
Attributes should check strings case sensitively 2/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Foobar''
```

### ブール値が「false」の属性は通過するはずである
``` ids attribute/pass-attributes_with_a_boolean_false_should_pass.ids
Attributes with a boolean false should pass
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''IsCritical''
```

### ブール値が「true」の属性は通過するはずである
``` ids attribute/pass-attributes_with_a_boolean_true_should_pass.ids
Attributes with a boolean true should pass
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''IsCritical''
```

### 論理値が「不明」の属性は、常に失敗する
``` ids attribute/fail-attributes_with_a_logical_unknown_always_fail.ids
Attributes with a logical unknown always fail
Entity: ''IFCPRESENTATIONLAYERWITHSTYLE''
Requirements:
Attribute: ''LayerOn''
```

### プリミティブを参照するselectを持つ属性は、次の条件を満たす必要があります
``` ids attribute/pass-attributes_with_a_select_referencing_a_primitive_should_pass.ids
Attributes with a select referencing a primitive should pass
Entity: ''IFCSURFACESTYLERENDERING''
Requirements:
Attribute: ''DiffuseColour''
```

### オブジェクトを参照するselectを持つ属性は、以下を満たす必要があります
``` ids attribute/pass-attributes_with_a_select_referencing_an_object_should_pass.ids
Attributes with a select referencing an object should pass
Entity: ''IFCSURFACESTYLERENDERING''
Requirements:
Attribute: ''DiffuseColour''
```

### 文字列値を持つ属性は、次の条件を満たす必要があります
``` ids attribute/pass-attributes_with_a_string_value_should_pass.ids
Attributes with a string value should pass
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### 持続時間がゼロの属性は通過すべきです
``` ids attribute/pass-attributes_with_a_zero_duration_should_pass.ids
Attributes with a zero duration should pass
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''ScheduleDuration''
```

### 数値がゼロの属性には意味があり、合格すべきである
``` ids attribute/pass-attributes_with_a_zero_number_have_meaning_and_should_pass.ids
Attributes with a zero number have meaning and should pass
Entity: ''IFCQUANTITYCOUNT''
Requirements:
Attribute: ''CountValue''
```

### リストが空の属性は常に失敗する
``` ids attribute/fail-attributes_with_an_empty_list_always_fail.ids
Attributes with an empty list always fail
Entity: ''IFCRELCONNECTSPATHELEMENTS''
Requirements:
Attribute: ''RelatingPriorities''
```

### 空集合を持つ属性は常に失敗する
``` ids attribute/fail-attributes_with_an_empty_set_always_fail.ids
Attributes with an empty set always fail
Entity: ''IFCPRESENTATIONLAYERWITHSTYLE''
Requirements:
Attribute: ''LayerStyles''
```

### 空の文字列を持つ属性は常に失敗する
``` ids attribute/fail-attributes_with_empty_strings_always_fail.ids
Attributes with empty strings always fail
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### null値を持つ属性は常に失敗する
``` ids attribute/fail-attributes_with_null_values_always_fail.ids
Attributes with null values always fail
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name''
```

### ブール値は小文字の文字列として指定する必要があります 1/3
``` ids attribute/fail-booleans_must_be_specified_as_lowercase_strings_1_3.ids
Booleans must be specified as lowercase strings 1/3
Entity: ''IFCTASK''
Requirements:
Attribute: ''IsMilestone'',''true''
```

### ブール値は小文字の文字列として指定する必要があります 2/3
``` ids attribute/invalid-booleans_must_be_specified_as_lowercase_strings_2_3.ids
Booleans must be specified as lowercase strings 2/3
Entity: ''IFCTASK''
Requirements:
Attribute: ''IsMilestone'',''FALSE''
```

### ブール値は小文字の文字列として指定する必要があります 3/3
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

### 派生属性は検証できず、常に失敗します
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

### 持続時間は文字列として扱われる 2/2
``` ids attribute/fail-durations_are_treated_as_strings_2_2.ids
Durations are treated as strings 2/2
IFC4
Entity: ''IFCTASKTIME''
Requirements:
Attribute: ''ScheduleDuration'',''PT16H''
```

### GlobalIds は文字列として扱われ、展開は行われません
``` ids attribute/pass-globalids_are_treated_as_strings_and_not_expanded.ids
GlobalIds are treated as strings and not expanded
Entity: ''IFCWALL''
Requirements:
Attribute: ''GlobalId'',''1hqIFTRjfV6AWq_bMtnZwI''
```

### IDSは、識別子などにおける文字列の切り捨てには対応していません
``` ids attribute/fail-ids_does_not_handle_string_truncation_such_as_for_identifiers.ids
IDS does not handle string truncation such as for identifiers
IFC4
Entity: ''IFCPERSON''
Requirements:
Attribute: ''Identification'',''123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345_extra_characters''
```

### 整数は、数字と同じルールに従います
``` ids attribute/pass-integers_follow_the_same_rules_as_numbers.ids
Integers follow the same rules as numbers
IFC4
Entity: ''IFCSTAIRFLIGHT''
Requirements:
Attribute: ''NumberOfRisers'',''42''
```

### 整数は浮動小数点数として表現することはできません 2/2
``` ids attribute/invalid-integers_cannot_be_expressed_as_floating_point_numbers_2_2.ids
Integers cannot be expressed as floating point numbers 2/2
IFC4
Entity: ''IFCSTAIRFLIGHT''
Requirements:
Attribute: ''NumberOfRisers'',''42.0''
```

### 無効な属性名は常にエラーとなります
IFCWALL型のエンティティには、ActingRole 属性がありません。

``` ids attribute/invalid-invalid_attribute_names_always_fail.ids
Invalid attribute names always fail
Entity: ''IFCWALL''
Requirements:
Attribute: ''ActingRole''
```

### 逆属性はチェックできず、常に失敗します
``` ids attribute/invalid-inverse_attributes_cannot_be_checked_and_always_fail.ids
Inverse attributes cannot be checked and always fail
Entity: ''IFCPERSON''
Requirements:
Attribute: ''EngagedIn''
```

### 名前の制限条件に一致する結果 1/3
``` ids attribute/pass-name_restrictions_will_match_any_result_1_3.ids
Name restrictions will match any result 1/3
Entity: ''IFCMATERIALLAYERSET''
Requirements:
Attribute: Pattern(''.*Name.*'')
```

### 名前の制限条件に一致する結果は です 2/3
``` ids attribute/pass-name_restrictions_will_match_any_result_2_3.ids
Name restrictions will match any result 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: Enumeration(''Name'',''Description'')
```

### 名前の制限条件に一致する結果が3件中3件見つかりました 3/3
``` ids attribute/pass-name_restrictions_will_match_any_result_3_3.ids
Name restrictions will match any result 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: Enumeration(''Name'',''Description'')
```

### 非ASCII文字はエンコードされずに処理されます
``` ids attribute/pass-non_ascii_characters_are_treated_without_encoding.ids
Non-ascii characters are treated without encoding
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''♫Don'tÄrgerhôtelЊет''
```

### 数値は型変換を用いてチェックされます 1/4
``` ids attribute/pass-numeric_values_are_checked_using_type_casting_1_4.ids
Numeric values are checked using type casting 1/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42''
```

### 数値は型変換を用いてチェックされる 2/4
``` ids attribute/pass-numeric_values_are_checked_using_type_casting_2_4.ids
Numeric values are checked using type casting 2/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42.''
```

### 数値は型変換を用いてチェックされる 3/4
``` ids attribute/pass-numeric_values_are_checked_using_type_casting_3_4.ids
Numeric values are checked using type casting 3/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42.0''
```

### 数値は型変換を用いてチェックされます 4/4
``` ids attribute/fail-numeric_values_are_checked_using_type_casting_4_4.ids
Numeric values are checked using type casting 4/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42''
```

### 特定の書式で表記された数値のみが許可されます 1/4
``` ids attribute/invalid-only_specifically_formatted_numbers_are_allowed_1_4.ids
Only specifically formatted numbers are allowed 1/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''42,3''
```

### 特定の書式で表記された数値のみが許可されます 2/4
``` ids attribute/invalid-only_specifically_formatted_numbers_are_allowed_2_4.ids
Only specifically formatted numbers are allowed 2/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''123,4.5''
```

### 特定の書式で表記された数値のみが許可されます 3/4
``` ids attribute/pass-only_specifically_formatted_numbers_are_allowed_3_4.ids
Only specifically formatted numbers are allowed 3/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''1.2345e3''
```

### 特定の形式で表記された数値のみが許可されます 4/4
``` ids attribute/pass-only_specifically_formatted_numbers_are_allowed_4_4.ids
Only specifically formatted numbers are allowed 4/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',''1.2345E3''
```

### 値が整数である場合に浮動小数点を指定することは無効です
IFC4では、属性名「`NumberOfRiser`」が「`NumberOfRisers`」に変更されている点にご注意ください。

``` ids attribute/invalid-specifying_a_float_when_the_value_is_an_integer_is_invalid.ids
Specifying a float when the value is an integer is invalid
IFC4
Entity: ''IFCSTAIRFLIGHT''
Requirements:
Attribute: Pattern(''NumberOfRiser(s)?''),''42.3''
```

### 範囲制限を設けることで、厳密な数値チェックを行うことができます
``` ids attribute/pass-strict_numeric_checking_may_be_done_with_a_bounds_restriction.ids
Strict numeric checking may be done with a bounds restriction
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''42'') MaxInclusive(''42'')
```

### 列挙型の制約内でも型チェックが行われる場合があります
列挙型で定義された型は、dataType と互換性がある必要があります。  
アトリビュートファセットの場合、dataType は IDS スキーマから取得されます。

ロードマップ：不整合な型は、監査ツールによって検出されるべきである。

``` ids attribute/pass-typecast_checking_may_also_occur_within_enumeration_restrictions.ids
Typecast checking may also occur within enumeration restrictions
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double Enumeration(''42'',''43'')
```

### リストの場合、値のチェックは常に失敗します
``` ids attribute/invalid-value_checks_always_fail_for_lists.ids
Value checks always fail for lists
Entity: ''IFCCARTESIANPOINT''
Requirements:
Attribute: ''Coordinates'',''Foobar''
```

### オブジェクトに対する値のチェックは常に失敗します
``` ids attribute/invalid-value_checks_always_fail_for_objects.ids
Value checks always fail for objects
IFC4
Entity: ''IFCTASK''
Requirements:
Attribute: ''TaskTime'',''Foobar''
```

### SELECT文では、値のチェックは常に失敗する
``` ids attribute/invalid-value_checks_always_fail_for_selects.ids
Value checks always fail for selects
Entity: ''IFCSURFACESTYLERENDERING''
Requirements:
Attribute: ''DiffuseColour'',''Foobar''
```

### 値の制限を使用できる 1/3
``` ids attribute/pass-value_restrictions_may_be_used_1_3.ids
Value restrictions may be used 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 値の制限は まで使用可能です 2/3
``` ids attribute/pass-value_restrictions_may_be_used_2_3.ids
Value restrictions may be used 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 値の制限は まで使用可能です 3/3
``` ids attribute/fail-value_restrictions_may_be_used_3_3.ids
Value restrictions may be used 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

## 分類
### データがないクラシフィケーションファセットは、クラシフィケーション1または2のいずれにも一致する 1/2
``` ids classification/fail-a_classification_facet_with_no_data_matches_any_classification_1_2.ids
A classification facet with no data matches any classification 1/2
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+'')
```

### データがないクラシフィケーションファセットは、どの分類とも一致する 2/2
``` ids classification/pass-a_classification_facet_with_no_data_matches_any_classification_2_2.ids
A classification facet with no data matches any classification 2/2
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+'')
```

### 禁止ファセットは、必須ファセットとは逆の結果を返します
``` ids classification/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCSLAB''
Requirements:
Classification: Prohibited,Pattern(''\w+'')
```

### 禁止されたクラシフィケーションファセット参照は、必須のファセットとは逆の結果を返します
``` ids classification/fail-a_prohibited_classification_reference_returns_the_opposite_of_a_required_facet.ids
A prohibited classification reference returns the opposite of a required facet
Entity: ''IFCSLAB''
Requirements:
Classification: Prohibited,''Foobar'',''1''
```

### 必須のファセットは、通常通りすべてのパラメータをチェックします
``` ids classification/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+'')
```

### 一致する項目がない場合、必須の分類システムは機能しない
``` ids classification/fail-a_required_classification_system_fails_if_no_match.ids
A required classification system fails if no match
Entity: ''IFCSLAB''
Requirements:
Classification: ''Foobar1''
```

### オプションの分類値が指定されている場合、それが通過する
``` ids classification/pass-an_optional_classification_value_passes_if_specified.ids
An optional classification value passes if specified
Entity: ''IFCWALL''
Requirements:
Classification: Optional,Pattern(''\w+''),''ExpectedValue''
```

### オプションの分類値がnullの場合、その値は通過する
``` ids classification/pass-an_optional_classification_value_passes_if_null.ids
An optional classification value passes if null
Entity: ''IFCWALL''
Requirements:
Classification: Optional,Pattern(''\w+''),''ExpectedValue''
```

### 一致する項目がない場合、オプションの分類値は失敗となります
``` ids classification/fail-an_optional_classification_value_fails_if_no_match.ids
An optional classification value fails if no match
Entity: ''IFCWALL''
Requirements:
Classification: Optional,Pattern(''\w+''),''ExpectedValue''
```

### 「system」と「value」の両方が一致している必要があります（いずれかではなく、すべて）。 1/2
``` ids classification/pass-both_system_and_value_must_match__all__not_any__if_specified_1_2.ids
Both system and value must match (all, not any) if specified 1/2
Entity: ''IFCSLAB''
Requirements:
Classification: ''Foobar'',''1''
```

### 「system」と「value」の両方が一致している必要があります（いずれかではなく、すべて）。指定された場合 2/2
``` ids classification/fail-both_system_and_value_must_match__all__not_any__if_specified_2_2.ids
Both system and value must match (all, not any) if specified 2/2
Entity: ''IFCCOLUMN''
Requirements:
Classification: ''Foobar'',''1''
```

### 外部分類参照を持つルート化されていないリソースも、同様に通過する必要があります
ifc4 以降、IFCEXTERNALREFERENCERELATIONSHIP は、IFCEXTERNALREFERENCEを任意のIFCRESOURCEOBJECTSELECT に関連付けることができます。

``` ids classification/pass-non_rooted_resources_that_have_external_classification_references_should_also_pass.ids
Non-rooted resources that have external classification references should also pass
IFC4
Entity: ''IFCMATERIAL''
Requirements:
Classification: Pattern(''\w+''),''1''
```

### 発生状況は、システムごとのタイプ分類に優先する 1/3
``` ids classification/pass-occurrences_override_the_type_classification_per_system_1_3.ids
Occurrences override the type classification per system 1/3
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+''),''11''
```

### 発生件数は、システムごとのタイプ分類よりも優先される 2/3
``` ids classification/fail-occurrences_override_the_type_classification_per_system_2_3.ids
Occurrences override the type classification per system 2/3
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+''),''22''
```

### 発生状況は、システムごとのタイプ分類に優先する 3/3
``` ids classification/pass-occurrences_override_the_type_classification_per_system_3_3.ids
Occurrences override the type classification per system 3/3
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''\w+''),''X''
```

### 制限はシステム に適用できます 1/2
``` ids classification/fail-restrictions_can_be_used_for_systems_1_2.ids
Restrictions can be used for systems 1/2
Entity: ''IFCWALL''
Requirements:
Classification: Pattern(''Foo.*'')
```

### 制限はシステム に適用できます 2/2
``` ids classification/pass-restrictions_can_be_used_for_systems_2_2.ids
Restrictions can be used for systems 2/2
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''Foo.*'')
```

### 制限は、値 に対して適用できます 1/3
``` ids classification/pass-restrictions_can_be_used_for_values_1_3.ids
Restrictions can be used for values 1/3
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+''),Pattern(''1.*'')
```

### 制限は、値 に対して適用できます 2/3
``` ids classification/pass-restrictions_can_be_used_for_values_2_3.ids
Restrictions can be used for values 2/3
Entity: ''IFCCOLUMN''
Requirements:
Classification: Pattern(''\w+''),Pattern(''1.*'')
```

### 制限は値 に適用できます 3/3
``` ids classification/fail-restrictions_can_be_used_for_values_3_3.ids
Restrictions can be used for values 3/3
Entity: ''IFCBEAM''
Requirements:
Classification: Pattern(''\w+''),Pattern(''1.*'')
```

### システムは と完全に一致する必要があります 1/5
``` ids classification/pass-systems_should_match_exactly_1_5.ids
Systems should match exactly 1/5
Entity: ''IFCPROJECT''
Requirements:
Classification: ''Foobar''
```

### システムは と完全に一致する必要があります 2/5
``` ids classification/fail-systems_should_match_exactly_2_5.ids
Systems should match exactly 2/5
Entity: ''IFCWALL''
Requirements:
Classification: ''Foobar''
```

### システムは と完全に一致する必要があります 3/5
``` ids classification/pass-systems_should_match_exactly_3_5.ids
Systems should match exactly 3/5
Entity: ''IFCSLAB''
Requirements:
Classification: ''Foobar''
```

### システムは と完全に一致する必要があります 4/5
``` ids classification/pass-systems_should_match_exactly_4_5.ids
Systems should match exactly 4/5
Entity: ''IFCCOLUMN''
Requirements:
Classification: ''Foobar''
```

### システムは5つすべてが完全に一致している必要があります 5/5
``` ids classification/pass-systems_should_match_exactly_5_5.ids
Systems should match exactly 5/5
Entity: ''IFCBEAM''
Requirements:
Classification: ''Foobar''
```

### 完全な分類が使用されている場合、値はサブ参照と一致します（例：EF_25_10 は EF_25_10_25、EF_25_10_30 などと一致するはずです）
``` ids classification/pass-values_match_subreferences_if_full_classifications_are_used__e_g__ef_25_10_should_match_ef_25_10_25__ef_25_10_30__etc_.ids
Values match subreferences if full classifications are used (e.g. EF_25_10 should match EF_25_10_25, EF_25_10_30, etc)
Entity: ''IFCBEAM''
Requirements:
Classification: Pattern(''\w+''),''2''
```

### 軽量分類を使用する場合は、値が完全に一致する必要があります
``` ids classification/pass-values_should_match_exactly_if_lightweight_classifications_are_used.ids
Values should match exactly if lightweight classifications are used
Entity: ''IFCSLAB''
Requirements:
Classification: Pattern(''\w+''),''1''
```

## エンティティ
### 一致するエンティティは、以下の条件を満たす必要があります
``` ids entity/pass-a_matching_entity_should_pass.ids
A matching entity should pass
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL''
```

### 対応する事前定義型は、以下の条件を満たす必要があります
``` ids entity/pass-a_matching_predefined_type_should_pass.ids
A matching predefined type should pass
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''SOLIDWALL''
```

### null 型の事前定義型は、指定された事前定義型に対して常に失敗するべきである
``` ids entity/fail-a_null_predefined_type_should_always_fail_a_specified_predefined_types.ids
A null predefined type should always fail a specified predefined types
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''SOLIDWALL''
```

### 列挙型から定義された事前定義型は、大文字でなければならない
``` ids entity/fail-a_predefined_type_from_an_enumeration_must_be_uppercase.ids
A predefined type from an enumeration must be uppercase
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''solidwall''
```

### 事前定義された型は、ユーザー定義の要素型を指定できる
``` ids entity/pass-a_predefined_type_may_specify_a_user_defined_element_type.ids
A predefined type may specify a user-defined element type
Entity: ''IFCWALLTYPE''
Requirements:
Entity: ''IFCWALLTYPE'',''WALDO''
```

### ユーザー定義の事前定義型を指定することができます
``` ids entity/pass-userdefined_predefined_types_may_be_specified.ids
Userdefined predefined types may be specified
Entity: ''IFCWALLTYPE''
Requirements:
Entity: ''IFCWALLTYPE'',''USERDEFINED''
```

### 事前定義型は、ユーザー定義オブジェクト型を指定できる
列挙型で「custom」が許可されている場合、このカスタムサブタイプも許可されるべきです。IfcWall には2X3 形式で predefinedType が定義されていないため、テストケースはIFC4に限定されます。


``` ids entity/pass-a_predefined_type_may_specify_a_user_defined_object_type.ids
A predefined type may specify a user-defined object type
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''WALDO''
```

### 事前定義された型は、ユーザー定義のプロセス型を指定できる
``` ids entity/pass-a_predefined_type_may_specify_a_user_defined_process_type.ids
A predefined type may specify a user-defined process type
IFC4
Entity: ''IFCTASKTYPE''
Requirements:
Entity: ''IFCTASKTYPE'',''TASKY''
```

### 指定された事前定義済み型に一致しないエンティティは失敗します
``` ids entity/fail-an_entity_not_matching_a_specified_predefined_type_will_fail.ids
An entity not matching a specified predefined type will fail
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''SOLIDWALL''
```

### 指定されたクラスに一致しないエンティティは失敗するべきである
``` ids entity/invalid-an_entity_not_matching_the_specified_class_should_fail.ids
An entity not matching the specified class should fail
Entity: ''IFCSLAB''
Requirements:
Entity: ''IFCWALL''
```

### 一致するエンティティは、事前定義された型にかかわらず通過すべきである
``` ids entity/pass-an_matching_entity_should_pass_regardless_of_predefined_type.ids
An matching entity should pass regardless of predefined type
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL''
```

### エンティティは、XSD正規表現パターンとして指定できます 1/2
``` ids entity/invalid-entities_can_be_specified_as_a_xsd_regex_pattern_1_2.ids
Entities can be specified as a XSD regex pattern 1/2
Entity: ''IFCWALL''
Requirements:
Entity: Pattern(''IFC.*TYPE'')
```

### エンティティは、XSD正規表現パターンとして指定できます 2/2
``` ids entity/pass-entities_can_be_specified_as_a_xsd_regex_pattern_2_2.ids
Entities can be specified as a XSD regex pattern 2/2
Entity: ''IFCWALLTYPE''
Requirements:
Entity: Pattern(''IFC.*TYPE'')
```

### エンティティは列挙型として指定できます 1/3
``` ids entity/pass-entities_can_be_specified_as_an_enumeration_1_3.ids
Entities can be specified as an enumeration 1/3
Entity: ''IFCWALL''
Requirements:
Entity: Enumeration(''IFCWALL'',''IFCSLAB'')
```

### エンティティは列挙型として指定できます 2/3
``` ids entity/pass-entities_can_be_specified_as_an_enumeration_2_3.ids
Entities can be specified as an enumeration 2/3
Entity: ''IFCSLAB''
Requirements:
Entity: Enumeration(''IFCWALL'',''IFCSLAB'')
```

### エンティティは列挙型として指定できます 3/3
``` ids entity/invalid-entities_can_be_specified_as_an_enumeration_3_3.ids
Entities can be specified as an enumeration 3/3
Entity: ''IFCBEAM''
Requirements:
Entity: Enumeration(''IFCWALL'',''IFCSLAB'')
```

### エンティティは、大文字の文字列として指定する必要があります
``` ids entity/invalid-entities_must_be_specified_as_uppercase_strings.ids
Entities must be specified as uppercase strings
Entity: ''IFCWALL''
Requirements:
Entity: ''IfcWall''
```

### IFC2X3では、タイプマッピングテーブル を通じて、AirTerminal を名前で照会することができます 1/2
[IFC2X3の発生およびタイプマッピングテーブル](../ifc2x3-occurrence-type-mapping-table.md)を使用すると、IFC2X3モデルを、IFC4のエンティティ名 `IfcAirTerminal`に対して直接検証を行うことができます。適用性は `IFCAIRTERMINAL`自体に対して表現され、これは実際のIFC2X3発生クラス `IfcFlowTerminal`（型指定元： `IfcAirTerminalType`、実際のIFC2X3オカレンスクラスに解決されます。実世界での一般的な要件である命名については、解決されたオカレンスに対してチェックが行われます。"すべてのAirTerminalは、AIR-XXXのような形式で命名される必要があります"）。







``` ids entity/pass-in_ifc2x3_an_airterminal_can_be_checked_by_name_via_the_type_mapping_table_1_2.ids
In IFC2X3 an AirTerminal can be checked by name via the type mapping table 1/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
Requirements:
Attribute: ''Name'',Pattern(''AIR-.*'')
```

### IFC2X3では、タイプマッピングテーブル を通じて、AirTerminal を名前で照会することができます 2/2
上記のケースと同じ仕様で、 `IfcFlowTerminal`（ `IfcAirTerminalType`定義されたIfcFlowTerminalに対して実行した結果、`Name`パターンと一致しないため、この失敗は適用可能性が未解決であることではなく、名称の不一致によるものです）。



``` ids entity/fail-in_ifc2x3_an_airterminal_can_be_checked_by_name_via_the_type_mapping_table_2_2.ids
In IFC2X3 an AirTerminal can be checked by name via the type mapping table 2/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
Requirements:
Attribute: ''Name'',Pattern(''AIR-.*'')
```

### IFC2X3では、タイプマッピングテーブル に基づき、AirTerminal が 1 つ存在しなければならない 1/2
適用性だけで、"モデル内にAirTerminalsが存在しなければならない"という条件を表現できます。仕様のデフォルトのカーディナリティは"必須"であるため、タイプマッピングテーブルを通じて `IFCAIRTERMINAL`に対して解決される要素がない場合、別途要件を定義する必要なく、この仕様は失敗となります。




``` ids entity/pass-in_ifc2x3_there_must_be_an_airterminal_per_the_type_mapping_table_1_2.ids
In IFC2X3 there must be an AirTerminal per the type mapping table 1/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
```

### IFC2X3では、タイプマッピングテーブル に基づき、AirTerminal が 1 つ存在しなければならない 2/2
上記のケースと同じ仕様で、以下の要素を含まないモデルに対して実行する `IfcFlowTerminal`が `IfcAirTerminalType`タイプが一切含まれていないモデルに対して実行したため、要件の不適合ではなく、適用可能なエンティティがゼロであるという理由で仕様が失敗します。




``` ids entity/fail-in_ifc2x3_there_must_be_an_airterminal_per_the_type_mapping_table_2_2.ids
In IFC2X3 there must be an AirTerminal per the type mapping table 2/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
```

### IFC2X3において、AirTerminal の定義済みタイプは、タイプマッピングテーブル を通じて解決されます 1/2
IFC2X3では、事前定義された型はインスタンスではなく、型オブジェクト上に存在します。適用性は、 `IFCAIRTERMINAL`型マッピングテーブルを通じて解決され、要件チェック `IfcAirTerminalType.PredefinedType`、名前付き列挙値に対してチェックされます。




``` ids entity/pass-in_ifc2x3_an_airterminal_predefined_type_resolves_via_the_type_mapping_table_1_2.ids
In IFC2X3 an AirTerminal predefined type resolves via the type mapping table 1/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
Requirements:
Entity: ''IFCAIRTERMINAL'',''DIFFUSER''
```

### IFC2X3において、AirTerminal の定義済み型は、型マッピングテーブル を通じて解決されます 2/2
上記のケースと同じ仕様で、 `IfcAirTerminalType``PredefinedType`異なる列挙値（`GRILLE`）実行したため、この失敗は未解決の適用可能性の問題ではなく、事前定義されたタイプの不一致によるものです。




``` ids entity/fail-in_ifc2x3_an_airterminal_predefined_type_resolves_via_the_type_mapping_table_2_2.ids
In IFC2X3 an AirTerminal predefined type resolves via the type mapping table 2/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
Requirements:
Entity: ''IFCAIRTERMINAL'',''DIFFUSER''
```

### IFC2X3において、ユーザー定義の AirTerminal 事前定義型は、型マッピングテーブル を通じて解決されます 1/2
`USERDEFINED` IFC2X3 では、の事前定義型には独自のニュアンスがあります。カスタムラベルは `IfcAirTerminalType.ElementType`、オカレンスの`ObjectType`には存在しません。この要件では、`PredefinedType`自体が`USERDEFINED`であるかどうかのみがチェックされます。




``` ids entity/pass-in_ifc2x3_a_user_defined_airterminal_predefined_type_resolves_via_the_type_mapping_table_1_2.ids
In IFC2X3 a user-defined AirTerminal predefined type resolves via the type mapping table 1/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
Requirements:
Entity: ''IFCAIRTERMINAL'',''USERDEFINED''
```

### IFC2X3において、ユーザー定義の AirTerminal 事前定義型は、型マッピングテーブル を通じて解決されます 2/2
上記のケースと同じ仕様で、 `IfcAirTerminalType`実行し、`USERDEFINED`代わりに`PredefinedType`（`DIFFUSER`）を使用した場合、この失敗は未解決の適用可能性の問題ではなく、事前定義されたタイプの不一致によるものです。




``` ids entity/fail-in_ifc2x3_a_user_defined_airterminal_predefined_type_resolves_via_the_type_mapping_table_2_2.ids
In IFC2X3 a user-defined AirTerminal predefined type resolves via the type mapping table 2/2
IFC2X3
Entity: ''IFCAIRTERMINAL''
Requirements:
Entity: ''IFCAIRTERMINAL'',''USERDEFINED''
```

### 継承された定義済み型は、次の条件を満たす必要があります
``` ids entity/pass-inherited_predefined_types_should_pass.ids
Inherited predefined types should pass
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''X''
```

### 無効なエンティティは常に失敗します
``` ids entity/invalid-invalid_entities_always_fail.ids
Invalid entities always fail
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCRABBIT''
```

### オーバーライドされた定義済み型は、以下の条件を満たす必要があります
``` ids entity/pass-overridden_predefined_types_should_pass.ids
Overridden predefined types should pass
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''X''
```

### 定義済み型 に対して制限を指定することができます 1/3
``` ids entity/pass-restrictions_can_be_specified_for_the_predefined_type_1_3.ids
Restrictions can be specified for the predefined type 1/3
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',Pattern(''FOO.*'')
```

### 定義済み型 に対して制限を指定することができます 2/3
``` ids entity/pass-restrictions_can_be_specified_for_the_predefined_type_2_3.ids
Restrictions can be specified for the predefined type 2/3
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',Pattern(''FOO.*'')
```

### 定義済み型 に対して制限を指定することができます 3/3
``` ids entity/fail-restrictions_can_be_specified_for_the_predefined_type_3_3.ids
Restrictions can be specified for the predefined type 3/3
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',Pattern(''FOO.*'')
```

### サブクラスは一致対象とはみなされません
``` ids entity/invalid-subclasses_are_not_considered_as_matching.ids
Subclasses are not considered as matching
Entity: ''IFCWALLSTANDARDCASE''
Requirements:
Entity: ''IFCWALL''
```

### ユーザー定義型は、大文字と小文字を区別してチェックされます
``` ids entity/fail-user_defined_types_are_checked_case_sensitively.ids
User-defined types are checked case sensitively
IFC4
Entity: ''IFCWALL''
Requirements:
Entity: ''IFCWALL'',''WALDO''
```

## ids
### 最小限のIDで、最小限のifc(1/2)を確認できます
``` ids ids/fail-a_minimal_ids_can_check_a_minimal_ifc_1_2.ids
A minimal ids can check a minimal ifc (1/2)
IFC4
Optional
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 最小限のIDであれば、最小限のifc(2/2)を確認できます
``` ids ids/pass-a_minimal_ids_can_check_a_minimal_ifc_2_2.ids
A minimal ids can check a minimal ifc (2/2)
IFC4
Optional
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 仕様は、すべての要件が満たされた場合にのみ合格となる（1/2）
``` ids ids/fail-a_specification_passes_only_if_all_requirements_pass_1_2.ids
A specification passes only if all requirements pass (1/2)
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
Attribute: ''Description'',''Foobar''
```

### 仕様は、すべての要件が満たされた場合にのみ合格となる（2/2）
``` ids ids/pass-a_specification_passes_only_if_all_requirements_pass_2_2.ids
A specification passes only if all requirements pass (2/2)
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
Attribute: ''Description'',''Foobar''
```

### 該当する項目がない場合でも、オプションの仕様は合格となる場合があります
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

### 適用条件が一致する場合、禁止仕様は失敗となります
``` ids ids/fail-prohibited_specifications_fails_if_the_applicability_matches.ids
Prohibited specifications fails if the applicability matches
Prohibited
IFC2X3
Entity: ''IFCWALL''
```

### 適用条件が一致しない場合、禁止仕様が通過してしまう
``` ids ids/pass-prohibited_specifications_passes_if_the_applicability_does_not_matches.ids
Prohibited specifications passes if the applicability does not matches
Prohibited
IFC2X3
Entity: ''IFCWINDOW''
```

### 必須仕様には、該当するエンティティが少なくとも1つ必要です（1/2）
``` ids ids/pass-required_specifications_need_at_least_one_applicable_entity_1_2.ids
Required specifications need at least one applicable entity (1/2)
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 必須仕様には、該当するエンティティが少なくとも1つ必要です（2/2）
``` ids ids/fail-required_specifications_need_at_least_one_applicable_entity_2_2.ids
Required specifications need at least one applicable entity (2/2)
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

### 仕様の選択性とファセットの選択性は組み合わせることができる
``` ids ids/pass-specification_optionality_and_facet_optionality_can_be_combined.ids
Specification optionality and facet optionality can be combined
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
Attribute: Optional,''Description'',''Foobar''
```

### 仕様バージョンはあくまでメタデータであり、合格・不合格の結果には影響しません
``` ids ids/pass-specification_version_is_purely_metadata_and_does_not_impact_pass_or_fail_result.ids
Specification version is purely metadata and does not impact pass or fail result
Optional
IFC2X3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',''Waldo''
```

## 素材
### データが含まれていない構成セットは、値のチェックに失敗します
``` ids material/fail-a_constituent_set_with_no_data_will_fail_a_value_check.ids
A constituent set with no data will fail a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 材料カテゴリは値のチェックに合格する場合がある
``` ids material/pass-a_material_category_may_pass_the_value_check.ids
A material category may pass the value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### データが含まれていない材料リストは、値のチェックに失敗します
``` ids material/fail-a_material_list_with_no_data_will_fail_a_value_check.ids
A material list with no data will fail a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 材料名は値のチェックを通過する場合がある
``` ids material/pass-a_material_name_may_pass_the_value_check.ids
A material name may pass the value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 禁止ファセットは、必須ファセットとは逆の結果を返します
``` ids material/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCWALL''
Requirements:
Material: Prohibited,
```

### 必須のファセットは、通常通りすべてのパラメータをチェックします
``` ids material/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
Material: 
```

### オプションの材料が指定された場合、その指定は有効となります
``` ids material/pass-an_optional_material_passes_if_specified.ids
An optional material passes if specified
Entity: ''IFCWALL''
Requirements:
Material: Optional,''Foo''
```

### オプションの材料がnullの場合、合格となる
``` ids material/pass-an_optional_material_passes_if_null.ids
An optional material passes if null
Entity: ''IFCWALL''
Requirements:
Material: Optional,''Foo''
```

### オプションの材料 について、一致する値がない場合は不適合となる
``` ids material/fail-an_optional_material_fails_if_no_value_matches.ids
An optional material fails if no value matches
Entity: ''IFCWALL''
Requirements:
Material: Optional,''Foo''
```

### 構成要素セット内のどの構成要素カテゴリも、値のチェックに合格します
``` ids material/pass-any_constituent_category_in_a_constituent_set_will_pass_a_value_check.ids
Any constituent Category in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 構成要素セット内の任意の構成要素名は、値のチェックに合格します
``` ids material/pass-any_constituent_name_in_a_constituent_set_will_pass_a_value_check.ids
Any constituent Name in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット内のどのレイヤーのカテゴリであっても、値のチェックを通過します
``` ids material/pass-any_layer_category_in_a_layer_set_will_pass_a_value_check.ids
Any layer Category in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット内のどのレイヤー名であっても、値のチェックを通過します
``` ids material/pass-any_layer_name_in_a_layer_set_will_pass_a_value_check.ids
Any layer Name in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 構成セット内のどのマテリアルカテゴリも、値のチェックに合格します
``` ids material/pass-any_material_category_in_a_constituent_set_will_pass_a_value_check.ids
Any material Category in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット内のどのマテリアルカテゴリでも、値のチェックに合格します
``` ids material/pass-any_material_category_in_a_layer_set_will_pass_a_value_check.ids
Any material Category in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### リスト内のどの「素材カテゴリ」でも、値のチェックを通過します
``` ids material/pass-any_material_category_in_a_list_will_pass_a_value_check.ids
Any material Category in a list will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイルセット内のどのマテリアルカテゴリも、値のチェックに合格します
``` ids material/pass-any_material_category_in_a_profile_set_will_pass_a_value_check.ids
Any material category in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 構成セットに含まれる任意のマテリアル名 については、値のチェックに合格します
``` ids material/pass-any_material_name_in_a_constituent_set_will_pass_a_value_check.ids
Any material Name in a constituent set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット内の任意のマテリアル名は、値のチェックに合格します
``` ids material/pass-any_material_name_in_a_layer_set_will_pass_a_value_check.ids
Any material Name in a layer set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### リスト内の任意の「Name」という名前の項目は、値のチェックを通過します
``` ids material/pass-any_material_name_in_a_list_will_pass_a_value_check.ids
Any material Name in a list will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイルセット内の「Name」という名前の項目はすべて、値のチェックに合格します
``` ids material/pass-any_material_name_in_a_profile_set_will_pass_a_value_check.ids
Any material Name in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイルセット内のどのプロファイルカテゴリでも、値のチェックに合格します
``` ids material/pass-any_profile_category_in_a_profile_set_will_pass_a_value_check.ids
Any profile Category in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### プロファイルセット内のプロファイル名はすべて、値のチェックに合格します
``` ids material/pass-any_profile_name_in_a_profile_set_will_pass_a_value_check.ids
Any profile Name in a profile set will pass a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### 任意のマテリアルを持つエレメントは、空のマテリアルファセットを通過します
``` ids material/pass-elements_with_any_material_will_pass_an_empty_material_facet.ids
Elements with any material will pass an empty material facet
Entity: ''IFCWALL''
Requirements:
Material: 
```

### 材質が指定されていない要素は、常に失敗する
``` ids material/fail-elements_without_a_material_always_fail.ids
Elements without a material always fail
Entity: ''IFCWALL''
Requirements:
Material: 
```

### データがないマテリアルは、値のチェックに失敗します
``` ids material/fail-material_with_no_data_will_fail_a_value_check.ids
Material with no data will fail a value check
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### インスタンスは、その型からマテリアルを継承することができます
``` ids material/pass-occurrences_can_inherit_materials_from_their_types.ids
Occurrences can inherit materials from their types
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### インスタンスは、そのタイプから指定されたマテリアルを上書きすることができます
``` ids material/pass-occurrences_can_override_materials_from_their_types.ids
Occurrences can override materials from their types
Entity: ''IFCWALL''
Requirements:
Material: ''Foo''
```

### レイヤーセット名は値のチェックに合格します
``` ids material/pass-a_layer_set_name_will_pass_a_value_check.ids
A layer set name will pass the value check
Entity: ''IFCWALL''
Requirements:
Material: ''Bar''
```

## の一部
### グループ内のエンティティは、1つまたは2つと厳密に一致しなければならない 1/2
``` ids partof/fail-a_group_entity_must_match_exactly_1_2.ids
A group entity must match exactly 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCGROUP'',IFCRELASSIGNSTOGROUP
```

### グループ内のエンティティは、 と完全に一致しなければならない 2/2
``` ids partof/pass-a_group_entity_must_match_exactly_2_2.ids
A group entity must match exactly 2/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCINVENTORY'',IFCRELASSIGNSTOGROUP
```

### グループの事前定義型は、 と完全に一致しなければならない 1/2
``` ids partof/invalid-a_group_predefined_type_must_match_exactly_1_2.ids
A group predefined type must match exactly 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCINVENTORY'',''BUNNARY'',IFCRELASSIGNSTOGROUP
```

### グループ事前定義型は、 と完全に一致する必要があります 2/2
``` ids partof/pass-a_group_predefined_type_must_match_exactly_2_2.ids
A group predefined type must match exactly 2/2
IFC4
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCINVENTORY'',''BUNNY'',IFCRELASSIGNSTOGROUP
```

### グループ化された要素は、グループ関係を継承する
``` ids partof/pass-a_grouped_element_passes_a_group_relationship.ids
A grouped element passes a group relationship
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELASSIGNSTOGROUP
```

### 集約されていない要素は、集約関係の検証に失敗します
``` ids partof/fail-a_non_aggregated_element_fails_an_aggregate_relationship.ids
A non aggregated element fails an aggregate relationship
Entity: ''IFCWALL''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### グループ化されていない要素は、グループ関係に適合しない
``` ids partof/fail-a_non_grouped_element_fails_a_group_relationship.ids
A non grouped element fails a group relationship
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELASSIGNSTOGROUP
```

### 禁止ファセットは、必須ファセットとは逆の結果を返します
``` ids partof/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCWALL''
Requirements:
PartOf: Prohibited,Pattern(''.*''),IFCRELAGGREGATES
```

### 必須のファセットは、通常通りすべてのパラメータをチェックします
``` ids partof/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### 集約エンティティは、その祖先となる任意のホールパスを受け継ぐことができます
``` ids partof/pass-an_aggregate_entity_may_pass_any_ancestral_whole_passes.ids
An aggregate entity may pass any ancestral whole passes
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCELEMENTASSEMBLY'',IFCRELAGGREGATES
```

### 集計値は、全体の に相当する実体を指定することができる 1/2
``` ids partof/pass-an_aggregate_may_specify_the_entity_of_the_whole_1_2.ids
An aggregate may specify the entity of the whole 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSLAB'',IFCRELAGGREGATES
```

### 集計では、全体を構成する要素を指定することができる 2/2
``` ids partof/fail-an_aggregate_may_specify_the_entity_of_the_whole_2_2.ids
An aggregate may specify the entity of the whole 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCWALL'',IFCRELAGGREGATES
```

### 集約型は、全体に対する事前定義された型を指定できる 1/2
``` ids partof/pass-an_aggregate_may_specify_the_predefined_type_of_the_whole_1_2.ids
An aggregate may specify the predefined type of the whole 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSLAB'',''BASESLAB'',IFCRELAGGREGATES
```

### 集約型は、全体としての事前定義済み型を指定することができます 2/2
``` ids partof/fail-an_aggregate_may_specify_the_predefined_type_of_the_whole_2_2.ids
An aggregate may specify the predefined type of the whole 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSLAB'',''SLABRADOR'',IFCRELAGGREGATES
```

### 含まれる要素はすべて、包含関係 を満たす 1/2
``` ids partof/fail-any_contained_element_passes_a_containment_relationship_1_2.ids
Any contained element passes a containment relationship 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### 含まれる要素はいずれも、 の包含関係を満たす 2/2
``` ids partof/pass-any_contained_element_passes_a_containment_relationship_2_2.ids
Any contained element passes a containment relationship 2/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### ネストされたパーツはすべて、ネスト関係を継承します
``` ids partof/pass-any_nested_part_passes_a_nest_relationship.ids
Any nested part passes a nest relationship
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: Pattern(''.*''),IFCRELNESTS
```

### ネストされた全体は、すべてネスト関係に違反する
``` ids partof/fail-any_nested_whole_fails_a_nest_relationship.ids
Any nested whole fails a nest relationship
IFC4
Entity: ''IFCFURNITURE''
Requirements:
PartOf: Pattern(''.*''),IFCRELNESTS
```

### ネストは間接的なものである可能性がある
``` ids partof/pass-nesting_may_be_indirect.ids
Nesting may be indirect
IFC4
Entity: ''IFCMECHANICALFASTENER''
Requirements:
PartOf: ''IFCFURNITURE'',IFCRELNESTS
```

### 集約される部分は、集約関係を渡します
``` ids partof/pass-the_aggregated_part_passes_an_aggregate_relationship.ids
The aggregated part passes an aggregate relationship
Entity: ''IFCWALL''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### 集約された全体は、集約関係を満たさない
``` ids partof/fail-the_aggregated_whole_fails_an_aggregate_relationship.ids
The aggregated whole fails an aggregate relationship
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: Pattern(''.*''),IFCRELAGGREGATES
```

### コンテナエンティティは、 と完全に一致する必要があります 1/2
``` ids partof/fail-the_container_entity_must_match_exactly_1_2.ids
The container entity must match exactly 1/2
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSITE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナエンティティは、 と完全に一致する必要があります 2/2
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

### コンテナは、指定された関係 を用いて関連付けられなければなりません 1/2
``` ids partof/pass-the_container_must_be_related_using_specified_relation_1_2.ids
The container must be related using specified relation 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSPACE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナは、指定された関係 を用いて関連付けられる必要があります 2/2
``` ids partof/fail-the_container_must_be_related_using_specified_relation_2_2.ids
The container must be related using specified relation 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCSPACE'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### 封じ込めは間接的なものとなる場合がある 1/2
``` ids partof/pass-the_containment_can_be_indirect_1_2.ids
The containment can be indirect 1/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCBUILDING'',IFCRELAGGREGATES
```

### 封じ込めは間接的なものとなる場合がある 2/2
``` ids partof/fail-the_containment_can_be_indirect_2_2.ids
The containment can be indirect 2/2
Entity: ''IFCBEAM''
Requirements:
PartOf: ''IFCBUILDING'',IFCRELAGGREGATES
```

### コンテナの定義済み型は、 と完全に一致する必要があります 1/2
``` ids partof/fail-the_container_predefined_type_must_match_exactly_1_2.ids
The container predefined type must match exactly 1/2
IFC4
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSPACE'',''WARREN'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### コンテナの事前定義型は、 と完全に一致する必要があります 2/2
``` ids partof/pass-the_container_predefined_type_must_match_exactly_2_2.ids
The container predefined type must match exactly 2/2
IFC4
Entity: ''IFCELEMENTASSEMBLY''
Requirements:
PartOf: ''IFCSPACE'',''BURROW'',IFCRELCONTAINEDINSPATIALSTRUCTURE
```

### ネストされたエンティティは、 と完全に一致する必要があります 1/2
``` ids partof/fail-the_nest_entity_must_match_exactly_1_2.ids
The nest entity must match exactly 1/2
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCBEAM'',IFCRELNESTS
```

### ネストされたエンティティは、 と完全に一致する必要があります 2/2
``` ids partof/pass-the_nest_entity_must_match_exactly_2_2.ids
The nest entity must match exactly 2/2
IFC4
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCFURNITURE'',IFCRELNESTS
```

### ネストされた定義済み型は、 と完全に一致する必要があります 1/2
``` ids partof/fail-the_nest_predefined_type_must_match_exactly_1_2.ids
The nest predefined type must match exactly 1/2
IFC4
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCFURNITURE'',''LITTERBOX'',IFCRELNESTS
```

### ネストされた定義済み型は、 と完全に一致する必要があります 2/2
``` ids partof/pass-the_nest_predefined_type_must_match_exactly_2_2.ids
The nest predefined type must match exactly 2/2
IFC4
Entity: ''IFCDISCRETEACCESSORY''
Requirements:
PartOf: ''IFCFURNITURE'',''WATERBOTTLE'',IFCRELNESTS
```

## プロパティ
### 論理上の未知数は一致しないものとみなされ、合格とはみなされません
IFCDURATION は IFC2x3には含まれていません

``` ids property/fail-a_logical_unknown_is_considered_false_and_will_not_pass.ids
A logical unknown is considered as not matching and will not pass
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLOGICAL
```

### 名前チェックでは、任意のプロパティと任意の文字列値が一致します
``` ids property/pass-a_name_check_will_match_any_property_with_any_string_value.ids
A name check will match any property with any string value
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 名前チェックでは、数量と値の組み合わせを問わず一致します
``` ids property/pass-a_name_check_will_match_any_quantity_with_any_value.ids
A name check will match any quantity with any value
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE
```

### 文字列として指定された数値は、文字列として扱われます
``` ids property/pass-a_number_specified_as_a_string_is_treated_as_a_string.ids
A number specified as a string is treated as a string
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''1''
```

### 禁止ファセットは、必須ファセットとは逆の結果を返します
``` ids property/fail-a_prohibited_facet_returns_the_opposite_of_a_required_facet.ids
A prohibited facet returns the opposite of a required facet
Entity: ''IFCWALL''
Requirements:
Property: Prohibited,''Foo_Bar'',''Foo''
```

### false に設定されたプロパティも値とみなされ、名前チェックを通過します
``` ids property/pass-a_property_set_to_false_is_still_considered_a_value_and_will_pass_a_name_check.ids
A property set to false is still considered a value and will pass a name check
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN
```

### true に設定されたプロパティは、名前チェックに合格します
``` ids property/pass-a_property_set_to_true_will_pass_a_name_check.ids
A property set to true will pass a name check
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN
```

### 必須のファセットは、通常通りすべてのパラメータをチェックします
``` ids property/pass-a_required_facet_checks_all_parameters_as_normal.ids
A required facet checks all parameters as normal
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 持続時間がゼロの時間が経過する
IFCDURATION は IFC2x3には含まれていません

``` ids property/pass-a_zero_duration_will_pass.ids
A zero duration will pass
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDURATION
```

### 条件に合致する物件はすべて、要件 を満たしている必要があります 1/3
``` ids property/pass-all_matching_properties_must_satisfy_requirements_1_3.ids
All matching properties must satisfy requirements 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,''x''
```

### 条件に合致する物件はすべて、要件2および3を満たしている必要があります 2/3
``` ids property/pass-all_matching_properties_must_satisfy_requirements_2_3.ids
All matching properties must satisfy requirements 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,''x''
```

### 条件に合致する物件はすべて、要件 を満たしている必要があります 3/3
``` ids property/fail-all_matching_properties_must_satisfy_requirements_3_3.ids
All matching properties must satisfy requirements 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,''x''
```

### 条件に合致するすべての物件セットは、要件 を満たさなければならない 1/3
``` ids property/pass-all_matching_property_sets_must_satisfy_requirements_1_3.ids
All matching property sets must satisfy requirements 1/3
Entity: ''IFCWALL''
Requirements:
Property: Pattern(''Foo_.*''),''Foo'',IFCLABEL
```

### 一致するすべてのプロパティセットは、要件2および3を満たさなければならない 2/3
``` ids property/fail-all_matching_property_sets_must_satisfy_requirements_2_3.ids
All matching property sets must satisfy requirements 2/3
Entity: ''IFCWALL''
Requirements:
Property: Pattern(''Foo_.*''),''Foo'',IFCLABEL
```

### 一致するすべてのプロパティセットは、要件 を満たさなければならない 3/3
``` ids property/pass-all_matching_property_sets_must_satisfy_requirements_3_3.ids
All matching property sets must satisfy requirements 3/3
Entity: ''IFCWALL''
Requirements:
Property: Pattern(''Foo_.*''),''Foo'',IFCLABEL
```

### 空の文字列は一致しないものとみなされ、合格とはなりません
``` ids property/fail-an_empty_string_is_considered_false_and_will_not_pass.ids
An empty string is considered not matching and will not pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### オプションのファセットは、結果にかかわらず常に通過する 1/2
``` ids property/pass-an_optional_facet_always_passes_regardless_of_outcome_1_2.ids
An optional facet always passes regardless of outcome 1/2
Entity: ''IFCWALL''
Requirements:
Property: Optional,''Foo_Bar'',''Foo'',IFCLABEL
```

### オプションのファセットは、結果にかかわらず常に通過する 2/2
``` ids property/pass-an_optional_facet_always_passes_regardless_of_outcome_2_2.ids
An optional facet always passes regardless of outcome 2/2
Entity: ''IFCWALL''
Requirements:
Property: Optional,''Foo_Bar'',''Bar'',IFCLABEL
```

### 範囲指定されたプロパティ内で一致する値がある場合、 が返されます 1/4
``` ids property/pass-any_matching_value_in_a_bounded_property_will_pass_1_4.ids
Any matching value in a bounded property will pass 1/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''1''
```

### 範囲指定されたプロパティ内で一致する値があれば、 を通過します 2/4
``` ids property/pass-any_matching_value_in_a_bounded_property_will_pass_2_4.ids
Any matching value in a bounded property will pass 2/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''5''
```

### 範囲指定されたプロパティ内で一致する値があれば、 を通過する 3/4
``` ids property/pass-any_matching_value_in_a_bounded_property_will_pass_3_4.ids
Any matching value in a bounded property will pass 3/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''3''
```

### 範囲指定されたプロパティ内で一致する値があれば、 を通過します 4/4
``` ids property/fail-any_matching_value_in_a_bounded_property_will_pass_4_4.ids
Any matching value in a bounded property will pass 4/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''2''
```

### リストプロパティ内の一致する値はすべて、 を返します 1/3
``` ids property/pass-any_matching_value_in_a_list_property_will_pass_1_3.ids
Any matching value in a list property will pass 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''X''
```

### リストプロパティ内の一致する値はすべて、 を通過します 2/3
``` ids property/pass-any_matching_value_in_a_list_property_will_pass_2_3.ids
Any matching value in a list property will pass 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Y''
```

### リストのプロパティ内の一致する値はすべて、 を通過します 3/3
``` ids property/fail-any_matching_value_in_a_list_property_will_pass_3_3.ids
Any matching value in a list property will pass 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Z''
```

### テーブルのプロパティに一致する値がある場合、 が返されます 1/3
``` ids property/pass-any_matching_value_in_a_table_property_will_pass_1_3.ids
Any matching value in a table property will pass 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''X''
```

### テーブルのプロパティに一致する値があれば、 を通過する 2/3
``` ids property/pass-any_matching_value_in_a_table_property_will_pass_2_3.ids
Any matching value in a table property will pass 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''1''
```

### テーブルのプロパティに一致する値があれば、 を通過します 3/3
``` ids property/fail-any_matching_value_in_a_table_property_will_pass_3_3.ids
Any matching value in a table property will pass 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Y''
```

### 列挙型プロパティ内のいずれかの値が一致する場合、 が返されます 1/3
``` ids property/pass-any_matching_value_in_an_enumerated_property_will_pass_1_3.ids
Any matching value in an enumerated property will pass 1/3
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Pset_WallCommon'',''Status'',IFCLABEL,''EXISTING''
```

### 列挙型プロパティ内の値が一致すれば、 を通過する 2/3
``` ids property/pass-any_matching_value_in_an_enumerated_property_will_pass_2_3.ids
Any matching value in an enumerated property will pass 2/3
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Pset_WallCommon'',''Status'',IFCLABEL,''DEMOLISH''
```

### 列挙型プロパティに一致する値がない場合、 で失敗します 3/3
``` ids property/fail-no_matching_value_in_an_enumerated_property_will_fail_3_3.ids
No matching value in an enumerated property will fail 3/3
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Pset_WallCommon'',''Status'',IFCLABEL,''NEW''
```

### ブール値は小文字の文字列として指定する必要があります 1/3
``` ids property/fail-booleans_must_be_specified_as_lowercase_strings_1_3.ids
Booleans must be specified as lowercase strings 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN,''true''
```

### ブール値は小文字の文字列として指定する必要があります 2/3
``` ids property/pass-booleans_must_be_specified_as_lowercase_strings_2_3.ids
Booleans must be specified as lowercase strings 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN,''false''
```

### ブール値は小文字の文字列として指定する必要があります 3/3
``` ids property/invalid-booleans_must_be_specified_as_lowercase_strings_3_3.ids
Booleans must be specified as lowercase strings 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCBOOLEAN,''FALSE''
```

### 複雑なプロパティはサポートされていません 1/2
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
IFCDURATION は IFC2x3には含まれていません

``` ids property/fail-durations_are_treated_as_strings_1_2.ids
Durations are treated as strings 1/2
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDURATION,''PT16H''
```

### 持続時間は文字列として扱われる 2/2
IFCDURATION は IFC2x3には含まれていません

``` ids property/pass-durations_are_treated_as_strings_2_2.ids
Durations are treated as strings 2/2
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCDURATION,''PT16H''
```

### 対応するpsetはあるがプロパティがない要素も失敗する
``` ids property/fail-elements_with_a_matching_pset_but_no_property_also_fail.ids
Elements with a matching pset but no property also fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### プロパティがない要素は常に失敗する
``` ids property/fail-elements_with_no_properties_always_fail.ids
Elements with no properties always fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### IDSは、識別子などにおける文字列の切り捨てには対応していません
``` ids property/fail-ids_does_not_handle_string_truncation_such_as_for_identifiers.ids
IDS does not handle string truncation such as for identifiers
IFC4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCIDENTIFIER,''123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345_extra_characters''
```

### 複数のプロパティが一致する場合、すべての値が要件1および2を満たしている必要があります 1/2
``` ids property/pass-if_multiple_properties_are_matched__all_values_must_satisfy_requirements_1_2.ids
If multiple properties are matched, all values must satisfy requirements 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,Enumeration(''x'',''y'')
```

### 複数のプロパティが一致する場合、すべての値が要件 を満たしている必要があります 2/2
``` ids property/fail-if_multiple_properties_are_matched__all_values_must_satisfy_requirements_2_2.ids
If multiple properties are matched, all values must satisfy requirements 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',Pattern(''Foo.*''),IFCLABEL,Enumeration(''x'',''y'')
```

### 整数値は型キャストを用いてチェックされる 1/4
``` ids property/pass-integer_values_are_checked_using_type_casting_1_4.ids
Integer values are checked using type casting 1/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42''
```

### 整数値は、小数点付き では保存できません 2/4
``` ids property/invalid-integer_values_cannot_be_stored_with_decimal_2_4.ids
Integer values cannot be stored with decimal 2/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42.''
```

### 整数値は、小数点付き（ ）の形式で保存することはできません 3/4
``` ids property/invalid-integer_values_cannot_be_stored_with_decimal_3_4.ids
Integer values cannot be stored with decimal 3/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42.0''
```

### 整数値は型キャストを用いてチェックされます 4/4
``` ids property/invalid-integer_values_are_checked_using_type_casting_4_4.ids
Integer values are checked using type casting 4/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCINTEGER,''42.3''
```

### IFC2X3では、拡張材料プロパティを通じて材料プロパティがサポートされています
Issue #435と併せて提案されました。IFC2X3の`IfcMaterial`、 `IfcExtendedMaterialProperties`を通じてプロパティを引き継いでいますが、 `IfcMaterialProperties`（そのエンティティが使用可能なプロパティリストを取得したのはIFC4 からです）。このケースは、IFC2X3 において、一般的なプロパティの仕組みが材料にまで適用されることを示す検証例です。





``` ids property/pass-material_properties_are_supported_under_ifc2x3_via_extendedmaterialproperties.ids
Material properties are supported under IFC2X3 via extended material properties
IFC2X3
Entity: ''IFCMATERIAL''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### IFC2X3では、指定されていない材料特性はエラーとなります
上記のケースと同じ仕様で、拡張プロパティを持たない材料に対して実行したため、誤った「合格」判定が、正しくチェックされた「欠如」と混同されることはなかった。



``` ids property/fail-material_properties_that_are_absent_fail_under_ifc2x3.ids
Material properties that are absent fail under IFC2X3
IFC2X3
Entity: ''IFCMATERIAL''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### 材料特性は、IFC_PH_0_D2A466Bを通じてIfcMaterialPropertiesでサポートされています
Issue #435と併せて提案されたものです。上記の2つのケースに対応するIFC4では、 `IfcMaterialDefinition`のプロパティが `IfcMaterialProperties`を通じてIFC4 のプロパティにアクセスできることを確認する。



``` ids property/pass-material_properties_are_supported_under_ifc4_via_ifcmaterialproperties.ids
Material properties are supported under IFC4 via IfcMaterialProperties
IFC4
Entity: ''IFCMATERIAL''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### IFC4では、指定されていない材料特性はエラーとなります
``` ids property/fail-material_properties_that_are_absent_fail_under_ifc4.ids
Material properties that are absent fail under IFC4
IFC4
Entity: ''IFCMATERIAL''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### IFCデータ型を指定するために、措置が用いられる 1/2
``` ids property/fail-measures_are_used_to_specify_an_ifc_data_type_1_2.ids
Measures are used to specify an IFC data type 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCTIMEMEASURE,''2''
```

### IFCデータ型 を指定するために、措置が用いられる 2/2
``` ids property/pass-measures_are_used_to_specify_an_ifc_data_type_2_2.ids
Measures are used to specify an IFC data type 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCTIMEMEASURE,''2''
```

### 非ASCII文字はエンコードされずに処理されます
``` ids property/pass-non_ascii_characters_are_treated_without_encoding.ids
Non-ascii characters are treated without encoding
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''♫Don'tÄrgerhôtelЊет''
```

### 特定の書式で表記された数値のみが許可されます 1/4
``` ids property/invalid-only_specifically_formatted_numbers_are_allowed_1_4.ids
Only specifically formatted numbers are allowed 1/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42,3''
```

### 特定の書式で表記された数値のみが許可されます 2/4
``` ids property/invalid-only_specifically_formatted_numbers_are_allowed_2_4.ids
Only specifically formatted numbers are allowed 2/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''123,4.5''
```

### 特定の書式で表記された数値のみが許可されます 3/4
``` ids property/pass-only_specifically_formatted_numbers_are_allowed_3_4.ids
Only specifically formatted numbers are allowed 3/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.2345e3''
```

### 特定の形式で表記された数値のみが許可されます 4/4
``` ids property/pass-only_specifically_formatted_numbers_are_allowed_4_4.ids
Only specifically formatted numbers are allowed 4/4
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.2345E3''
```

### 事前定義されたプロパティはサポートされていますが、使用は推奨されません 1/2
``` ids property/pass-predefined_properties_are_supported_but_discouraged_1_2.ids
Predefined properties are supported but discouraged 1/2
Entity: ''IFCDOOR''
Requirements:
Property: ''Foo_Bar'',''PanelOperation'',IFCDOORPANELOPERATIONENUM,''SWINGING''
```

### 事前定義されたプロパティはサポートされていますが、使用は推奨されません 2/2
``` ids property/fail-predefined_properties_are_supported_but_discouraged_2_2.ids
Predefined properties are supported but discouraged 2/2
Entity: ''IFCDOOR''
Requirements:
Property: ''Foo_Bar'',''PanelOperation'',IFCDOORPANELOPERATIONENUM,''SWONGING''
```

### IFC4では、IfcContextを通じてプロジェクトプロパティがサポートされています
Issue #435 と同時に提案されました。 `IfcProject`は、 `IfcObject` IFC2X3内のから、IFC4 内の新しい `IfcContext`のサブタイプとして変更されました。 `IfcContext`、独自の`IsDefinedBy`個別に宣言しているため、プロパティ検索のために `IfcObject`プロパティ検索の特例として扱う実装であっても、 `IfcContext`カバーしない場合、IFC4上のプロパティを見つけることはできません。 `IfcProject` 上のプロパティを見つけることはできません。






``` ids property/pass-project_properties_are_supported_under_ifc4_via_ifccontext.ids
Project properties are supported under IFC4 via IfcContext
IFC4
Entity: ''IFCPROJECT''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### 存在しないプロジェクトプロパティは、IFC4経由でIfcContextによりエラーとなります
上記のケースと同じ仕様で、プロパティのないプロジェクトに対して実行したため、誤った「合格」が、正しくチェックされた「なし」と混同されることはなかった。



``` ids property/fail-project_properties_that_are_absent_fail_under_ifc4_via_ifccontext.ids
Project properties that are absent fail under IFC4 via IfcContext
IFC4
Entity: ''IFCPROJECT''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### IFC2X3では、IfcObjectを通じてプロジェクトプロパティがサポートされています
上記の2つのケースにおけるIFC2X3コントロール： `IfcProject`は単なる `IfcObject`と同じであるため、これはすでに動作しているはずのケースであり、IFC4のケースこそが注目すべきものであることを裏付けています。



``` ids property/pass-project_properties_are_supported_under_ifc2x3_via_ifcobject.ids
Project properties are supported under IFC2X3 via IfcObject
IFC2X3
Entity: ''IFCPROJECT''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### 存在しないプロジェクトプロパティは、IfcObjectを経由してIFC2X3でエラーとなる
``` ids property/fail-project_properties_that_are_absent_fail_under_ifc2x3_via_ifcobject.ids
Project properties that are absent fail under IFC2X3 via IfcObject
IFC2X3
Entity: ''IFCPROJECT''
Requirements:
Property: ''Custom_Pset'',''Foo'',IFCLABEL
```

### プロパティは型 から継承できます 1/2
``` ids property/pass-properties_can_be_inherited_from_the_type_1_2.ids
Properties can be inherited from the type 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### プロパティは型 から継承できます 2/2
``` ids property/pass-properties_can_be_inherited_from_the_type_2_2.ids
Properties can be inherited from the type 2/2
Entity: ''IFCWALLTYPE''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### プロパティはインスタンスによって上書きされることがあります 1/2
``` ids property/pass-properties_can_be_overriden_by_an_occurrence_1_2.ids
Properties can be overriden by an occurrence 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### プロパティはインスタンスによって上書きされることがあります 2/2
``` ids property/fail-properties_can_be_overriden_by_an_occurrence_2_2.ids
Properties can be overriden by an occurrence 2/2
Entity: ''IFCWALLTYPE''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 値がNULLのプロパティは失敗します
``` ids property/fail-properties_with_a_null_value_fail.ids
Properties with a null value fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 数量も、適切な単位と一致している必要があります
``` ids property/fail-quantities_must_also_match_the_appropriate_measure.ids
Quantities must also match the appropriate measure
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCAREAMEASURE
```

### 型変換を用いて実数値のチェックを行う 1/3
``` ids property/pass-real_values_are_checked_using_type_casting_1_3.ids
Real values are checked using type casting 1/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42''
```

### 型変換を用いた実数の検証 2/3
``` ids property/pass-real_values_are_checked_using_type_casting_2_3.ids
Real values are checked using type casting 2/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42.0''
```

### 型キャストを使用して実数値のチェックを行う 3/3
``` ids property/pass-real_values_are_checked_using_type_casting_3_3.ids
Real values are checked using type casting 3/3
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''42.3''
```

### 参照プロパティはオブジェクトとして扱われるため、サポートされていません
``` ids property/fail-reference_properties_are_treated_as_objects_and_not_supported.ids
Reference properties are treated as objects and not supported
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL
```

### 値の指定が、異なる値に対して失敗する
``` ids property/fail-specifying_a_value_fails_against_different_values.ids
Specifying a value fails against different values
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 値を指定すると、大文字と小文字を区別した一致が行われます 1/2
``` ids property/pass-specifying_a_value_performs_a_case_sensitive_match_1_2.ids
Specifying a value performs a case-sensitive match 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 値を指定すると、大文字と小文字を区別した一致が行われます 2/2
``` ids property/fail-specifying_a_value_performs_a_case_sensitive_match_2_2.ids
Specifying a value performs a case-sensitive match 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLABEL,''Bar''
```

### 単位の換算は、IDSが指定した標準単位に基づいて行うものとする 1/2
``` ids property/fail-unit_conversions_shall_take_place_to_ids_nominated_standard_units_1_2.ids
Unit conversions shall take place to IDS-nominated standard units 1/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''2''
```

### 単位の換算は、IDSが指定した標準単位に基づいて行うものとする 2/2
``` ids property/pass-unit_conversions_shall_take_place_to_ids_nominated_standard_units_2_2.ids
Unit conversions shall take place to IDS-nominated standard units 2/2
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCLENGTHMEASURE,''2''
```

### プロパティは、関連するオブジェクト型に関連付けることができます
この監査ツールは、予約済みプレフィックス「`Pset_`」で始まるプロパティを適切なオブジェクトに限定していますが、これらのプロパティは関連するタイプにも関連付けることができます。例えば、 `Pset_WallCommon`. `IFCWALLTYPE` 上の Pset_WallCommon。


提供されたIFCは、プロパティセットの 1 つで無効な値「`FOOBAR`」が定義されているため、エラーとなります。

``` ids property/fail-properties_can_be_associated_to_relevant_object_types.ids
Properties can be associated to relevant object types
Optional
IFC4
Entity: ''IFCWALLTYPE''
Requirements:
Property: ''Pset_WallCommon'',''FireRating'',IFCLABEL,Pattern(''(-|[0-9]{2,3})\/(-|[0-9]{2,3})\/(-|[0-9]{2,3})'')
```

## 制限
### 境界は排他的である場合がある 1/3
``` ids restriction/fail-a_bound_can_be_exclusive_1_3.ids
A bound can be exclusive 1/3
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinExclusive(''0'') MaxExclusive(''10'')
```

### 区間には を含むものもある 1/4
``` ids restriction/pass-a_bound_can_be_inclusive_1_4.ids
A bound can be inclusive 1/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### 境界は排他的 となり得る 2/3
``` ids restriction/pass-a_bound_can_be_exclusive_2_3.ids
A bound can be exclusive 2/3
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinExclusive(''0'') MaxExclusive(''10'')
```

### 区間は両端を含む場合がある 2/4
``` ids restriction/pass-a_bound_can_be_inclusive_2_4.ids
A bound can be inclusive 2/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### バウンドは排他的 となり得る 3/3
``` ids restriction/fail-a_bound_can_be_exclusive_3_3.ids
A bound can be exclusive 3/3
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinExclusive(''0'') MaxExclusive(''10'')
```

### 区間には、 を含むものもある 3/4
``` ids restriction/pass-a_bound_can_be_inclusive_3_4.ids
A bound can be inclusive 3/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### 境界は を含む場合がある 4/4
``` ids restriction/fail-a_bound_can_be_inclusive_4_4.ids
A bound can be inclusive 4/4
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',xs:double MinInclusive(''0'') MaxInclusive(''10'')
```

### 列挙では大文字と小文字が区別されます 1/3
``` ids restriction/pass-an_enumeration_matches_case_sensitively_1_3.ids
An enumeration matches case sensitively 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 列挙では、大文字と小文字が区別されます 2/3
``` ids restriction/pass-an_enumeration_matches_case_sensitively_2_3.ids
An enumeration matches case sensitively 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 列挙は、大文字と小文字を区別して一致します 3/3
``` ids restriction/fail-an_enumeration_matches_case_sensitively_3_3.ids
An enumeration matches case sensitively 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 列挙では大文字と小文字が区別されます 4/3
``` ids restriction/fail-an_enumeration_matches_case_sensitively_4_3.ids
An enumeration matches case sensitively 4/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Enumeration(''Foo'',''Bar'')
```

### 長さの確認は で使用できます 1/2
``` ids restriction/fail-length_checks_can_be_used_1_2.ids
Length checks can be used 1/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Length(''2'')
```

### 長さのチェックは で使用できます 2/2
``` ids restriction/pass-length_checks_can_be_used_2_2.ids
Length checks can be used 2/2
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Length(''2'')
```

### 最大・最小長さのチェックは、 で使用できます 1/3
``` ids restriction/fail-max_and_min_length_checks_can_be_used_1_3.ids
Max and min length checks can be used 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### 最大・最小長さのチェックは で使用できます 2/3
``` ids restriction/pass-max_and_min_length_checks_can_be_used_2_3.ids
Max and min length checks can be used 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### 最大・最小長さのチェックは で使用可能です 3/3
``` ids restriction/pass-max_and_min_length_checks_can_be_used_3_3.ids
Max and min length checks can be used 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### 最大・最小長さのチェックは で使用できます 4/3
``` ids restriction/fail-max_and_min_length_checks_can_be_used_4_3.ids
Max and min length checks can be used 4/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',MinLength(''2'') MaxLength(''3'')
```

### パターンは、どのような数値であっても常に無効です
``` ids restriction/invalid-patterns_always_fail_on_any_number.ids
Patterns always invalid on any number
Optional
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',Pattern(''.*'')
```

### パターンは文字列に対してのみ機能し、それ以外には機能しません
``` ids restriction/invalid-patterns_only_work_on_strings_and_nothing_else.ids
Patterns only work on strings and nothing else
Entity: ''IFCSURFACESTYLEREFRACTION''
Requirements:
Attribute: ''RefractionIndex'',Pattern(''.*'')
```

### 正規表現パターンは、 で使用できます 1/3
``` ids restriction/pass-regex_patterns_can_be_used_1_3.ids
Regex patterns can be used 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンは まで使用できます 2/3
``` ids restriction/pass-regex_patterns_can_be_used_2_3.ids
Regex patterns can be used 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンは で使用できます 3/3
``` ids restriction/fail-regex_patterns_can_be_used_3_3.ids
Regex patterns can be used 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現のパターンは「OR」で機能する 1/3
``` ids restriction/pass-regex_patterns_work_in_OR_1_3.ids
Regex patterns work in OR 1/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[A-Z]{2}[0-9]{2}'') Pattern(''[a-z]{2}[0-9]{2}'')
```

### 正規表現のパターンは「OR」で機能します 2/3
``` ids restriction/pass-regex_patterns_work_in_OR_2_3.ids
Regex patterns work in OR 2/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[a-z]{2}[0-9]{2}'') Pattern(''[A-Z]{2}[0-9]{2}'')
```

### 正規表現パターンは OR で機能します 3/3
``` ids restriction/fail-regex_patterns_work_in_OR_3_3.ids
Regex patterns work in OR 3/3
Entity: ''IFCWALL''
Requirements:
Attribute: ''Name'',Pattern(''[a-z]{3}[0-9]{2}'') Pattern(''[A-Z]{3}[0-9]{2}'')
```

## 寛容さ
### 浮動小数点数の正の大きな数値の下限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_high_number_lower_bound.ids
Comparison tolerance for floating point positive high number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点数の正の大きな数値の下限に関する比較許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_high_number_lower_bound.ids
Comparison tolerance for floating point positive high number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点数の正の大きな数値の上限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_high_number_upper_bound.ids
Comparison tolerance for floating point positive high number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点数の正の大きな数値の上限に関する比較許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_high_number_upper_bound.ids
Comparison tolerance for floating point positive high number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''100000.''
```

### 浮動小数点数の比較許容誤差：下限値の不一致
``` ids tolerance/fail-comparison_tolerance_for_floating_point_one_lower_bound.ids
Comparison tolerance for floating point one lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点数の下限判定1回分の比較許容誤差
``` ids tolerance/pass-comparison_tolerance_for_floating_point_one_lower_bound.ids
Comparison tolerance for floating point one lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点数の上限1回通過における比較許容誤差
``` ids tolerance/pass-comparison_tolerance_for_floating_point_one_upper_bound.ids
Comparison tolerance for floating point one upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点数の比較許容誤差：上限超過エラーが1件発生
``` ids tolerance/fail-comparison_tolerance_for_floating_point_one_upper_bound.ids
Comparison tolerance for floating point one upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''1.''
```

### 浮動小数点数の正の小さい数値の下限に関する比較許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_low_number_lower_bound.ids
Comparison tolerance for floating point positive low number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点数の正の小さい数値の下限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_low_number_lower_bound.ids
Comparison tolerance for floating point positive low number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点数の正の小さい数値の上限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_positive_low_number_upper_bound.ids
Comparison tolerance for floating point positive low number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点数の正の小さい数値の上限に関する比較許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_positive_low_number_upper_bound.ids
Comparison tolerance for floating point positive low number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.0000001''
```

### 浮動小数点数の下限がゼロである場合の比較許容誤差の違反
``` ids tolerance/fail-comparison_tolerance_for_floating_point_zero_lower_bound.ids
Comparison tolerance for floating point zero lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点数の下限がゼロである場合の許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_zero_lower_bound.ids
Comparison tolerance for floating point zero lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点ゼロの上限通過に対する比較許容誤差
``` ids tolerance/pass-comparison_tolerance_for_floating_point_zero_upper_bound.ids
Comparison tolerance for floating point zero upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点数のゼロの上限に関する比較許容誤差の違反
``` ids tolerance/fail-comparison_tolerance_for_floating_point_zero_upper_bound.ids
Comparison tolerance for floating point zero upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''0.''
```

### 浮動小数点負の最小値の下限逸脱に対する許容誤差
``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_low_number_lower_bound.ids
Comparison tolerance for floating point negative low number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負の低数値の下限通過に対する許容誤差
``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_low_number_lower_bound.ids
Comparison tolerance for floating point negative low number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負の最小値の上限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_low_number_upper_bound.ids
Comparison tolerance for floating point negative low number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点負の最小値の上限に関する比較許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_low_number_upper_bound.ids
Comparison tolerance for floating point negative low number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-0.0000001''
```

### 浮動小数点数の負の1の下限逸脱に対する比較許容誤差
``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_one_lower_bound.ids
Comparison tolerance for floating point negative one lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点数「-1」の下限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_one_lower_bound.ids
Comparison tolerance for floating point negative one lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点数「-1」の上限通過に対する比較許容誤差
``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_one_upper_bound.ids
Comparison tolerance for floating point negative one upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点数「-1」の上限比較における許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_one_upper_bound.ids
Comparison tolerance for floating point negative one upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1.''
```

### 浮動小数点負の大きな数値の下限超過に関する比較許容誤差
``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_high_number_lower_bound.ids
Comparison tolerance for floating point negative high number lower bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### 浮動小数点負の大きな数値の下限通過に関する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_high_number_lower_bound.ids
Comparison tolerance for floating point negative high number lower bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### 浮動小数点負の大きな数値の上限通過に対する許容誤差の比較
``` ids tolerance/pass-comparison_tolerance_for_floating_point_negative_high_number_upper_bound.ids
Comparison tolerance for floating point negative high number upper bound pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### 浮動小数点負の大きな数値の上限に関する比較許容誤差の失敗
``` ids tolerance/fail-comparison_tolerance_for_floating_point_negative_high_number_upper_bound.ids
Comparison tolerance for floating point negative high number upper bound fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,''-1000000.''
```

### ゼロより大きい浮動小数点範囲の比較許容誤差（ゼロは含まない）が許容範囲を超えた場合
``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_greater_than_zero_exclusive.ids
Comparison tolerance for floating point range greater than zero exclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinExclusive(''0.'')
```

### ゼロより大きい浮動小数点範囲の比較許容誤差（ゼロを除く）
``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_greater_than_zero_exclusive.ids
Comparison tolerance for floating point range greater than zero exclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinExclusive(''0.'')
```

### ゼロ以上を含む浮動小数点数の範囲に対する比較許容誤差が失敗した
``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_greater_than_zero_inclusive.ids
Comparison tolerance for floating point range greater than zero inclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinInclusive(''0.'')
```

### ゼロ以上（ゼロを含む）の浮動小数点範囲に対する比較許容誤差が合格基準を満たす
``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_greater_than_zero_inclusive.ids
Comparison tolerance for floating point range greater than zero inclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MinInclusive(''0.'')
```

### ゼロ未満の浮動小数点範囲に対する比較許容誤差が許容範囲を下回った場合、失敗とする
``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_lower_than_zero_exclusive.ids
Comparison tolerance for floating point range lower than zero exclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxExclusive(''0.'')
```

### ゼロ未満（ゼロを除く）の浮動小数点範囲に対する比較許容誤差
``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_lower_than_zero_exclusive.ids
Comparison tolerance for floating point range lower than zero exclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxExclusive(''0.'')
```

### ゼロ以下（ゼロを含む）の浮動小数点範囲に対する比較許容誤差が満たされない場合、失敗となる
``` ids tolerance/fail-comparison_tolerance_for_floating_point_range_lower_than_zero_inclusive.ids
Comparison tolerance for floating point range lower than zero inclusive fail
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxInclusive(''0.'')
```

### ゼロ以下を含む浮動小数点範囲の比較許容誤差が「合格」となる場合
``` ids tolerance/pass-comparison_tolerance_for_floating_point_range_lower_than_zero_inclusive.ids
Comparison tolerance for floating point range lower than zero inclusive pass
Entity: ''IFCWALL''
Requirements:
Property: ''Foo_Bar'',''Foo'',IFCREAL,xs:double MaxInclusive(''0.'')
```
