<script>
	import Reports from '../../components/Reports.svelte';
	import SecondaryHeader from '../../components/SecondaryHeader.svelte';
	import Themes from '../../components/Themes.svelte';
	import Ideas from '../../components/Ideas.svelte';
	import SettingsContainer from '../../components/SettingsContainer.svelte';
	import Languages from '../../components/Languages.svelte';
</script>

<SecondaryHeader></SecondaryHeader>
<SettingsContainer>
	<Themes></Themes>
	<Languages></Languages>
	<Reports></Reports>
	<Ideas></Ideas>
</SettingsContainer>
