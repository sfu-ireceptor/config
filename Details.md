# iReceptor AIRR Mapping Specifics

This configuration file is targeted at mapping repository informaction from the
iReceptor Turnkey v1 to the iReceptor Turnkey v2. This
configuration file can be used to map the data in an iReceptor Turnkey v1 repository
to work with the AIRR Data Commons API based service that is included with the
iReceptor Turnkey v2. The differences listed below are differences from the primary
v2 iReceptor Turnkey AIRR Mapping configuration file.

The changes are listed below:

- Row `repertoire_id` (column ir_id): repertoire_id is the main linking field between repertoires and rearrangements in the ADC API. In v1 this field is stored in the repository as \_id (column ir_repository) and as type integer (column ir_repository_type).
- Row `ir_junction_length_aa` (column ir_id): iReceptor has always stored this field, in v1 it was with an ir_ prefix. This field has been promoted to an AIRR field so we need to tell the service that the repository field is ir_junction_aa_length (column ir_repository).
- Row `repertoire_id_rearrangement` (column ir_id): This is the rearrangement field that contains the foreign key to the repertoire that this rearrangement belongs. In v1, like repertoire_id above, this is an integer (column ir_repository_type) and stored in the repository with the field name ir_project_sample_id (column ir_repository).
- Row `sample_processing_id, ir_record_number` (column ir_id): This is a new field that exists in the AIRR Standard that identifies a unique Sample Processing process within a Repertoire. In v1, iReceptor had a similar concept, and this is represented in the repository as an integer (column ir_repository_type) with the field name ir_record_number (column ir_repository). In addition, it is necessary to change the value in ir_repository column for ir_record_number so that there are not two mappings for this field. 
- Row `data_processing_id` (column ir_id): This is a new field that exists in the AIRR Standard that identifies a unique Data Processing process within a Repertoire. In v1, iReceptor had a similar concept, and this is represented in the repository as an integer (column ir_repository_type) with the field name ir_rearrangement_number (column ir_repository). In addition, it is necessary to change the value in ir_repository column for ir_rearrangement_number so that there are not two mappings for this field.
- Rows `ir_substring, ir_vgene_gene, ir_vgene_family, ir_jgene_gene, ir_jgene_family, ir_dgene_gene, ir_dgene_family` (column ir_id): These are fields that existed in v1 as custom iReceptor fields (hence the \_ir prefix) but have been promoted to AIRR fields. As a result, they need to be added to fields that the service returns (column service_name) so there are returned as part of the AIRR response.
- Row `ir_rearrangement_file_name` (column ir_id): This field holds a list of the files that were produced by the annotation tools used to generate the rearrangements. In v1 this is a string (column ir_repository_type) stored in the field name ir_rearrangement_file_name (column ir_repository) and rather than containing an array of strings, it is a comma separated list of filenames (indicated by the column ir_repository_is_array being False).
- Row `ir_subject_age_min, ir_subject_age_max` (column ir_id): iReceptor has always tracked an age range, but only recently did the AIRR standard incorporate this. As such, it is necessary to map the two AIRR age_min and age_max fields to the ir_min_age and ir_max_age fields in the repository respectively (column ir_repository).
- Row `filename` (column ir_id): The new filename field in the AIRR standard needs to be mapped to the iReceptor v1 ir_fasta_file_name field in the existing repository (column ir_repository)
- Row `germline_database` (column ir_id): The new germline_database field in the AIRR standard needs to be mapped to the iReceptor v1 field ir_germline_database (column ir_repository)
