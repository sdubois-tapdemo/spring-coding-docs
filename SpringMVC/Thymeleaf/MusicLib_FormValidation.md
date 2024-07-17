# MusicLib - iTunes Search API Wrapper

(iTunes Search API]https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/iTuneSearchAPI/LookupExamples.html#//apple_ref/doc/uid/TP40017632-CH7-SW1)

## JPA Project Setup
```
src/
├── main/
│   └── java/
|       ├── MusicLibApplication.java
|       ├── service/
|       |   └── ITunesService.java
|       ├── controller/
|       |   └── ITunesController.java
|       └── model/
|           ├── Artist.java
|           ├── Album.java
|           ├── ITunesEntity.java
|           └── ITunesResult.java
└── resources/
    |-- templates/
    |     └── student-confirmation.html
    |     └── student-form.html
    └── application.properties
```

## Model
### Artist (Artist.java)
```
package com.coresoftware.MusicLib.model;

public class Artist extends ITunesEntity {
	private String artistName;
	private String artistType;
	private String artistLinkUrl;
	private Integer artistId;
	private Integer amgArtistId;
	private String primaryGenreName;
	private Integer primaryGenreId;

	public final String wrapperType = "artist";

	public String getArtistName() {
		return artistName;
	}

	public void setArtistName(String artistName) {
		this.artistName = artistName;
	}

	public String getArtistType() {
		return artistType;
	}

	public void setArtistType(String artistType) {
		this.artistType = artistType;
	}

	public String getArtistLinkUrl() {
		return artistLinkUrl;
	}

	public void setArtistLinkUrl(String artistLinkUrl) {
		this.artistLinkUrl = artistLinkUrl;
	}

	public Integer getArtistId() {
		return artistId;
	}

	public void setArtistId(Integer artistId) {
		this.artistId = artistId;
	}

	public Integer getAmgArtistId() {
		return amgArtistId;
	}

	public void setAmgArtistId(Integer amgArtistId) {
		this.amgArtistId = amgArtistId;
	}

	public String getPrimaryGenreName() {
		return primaryGenreName;
	}

	public void setPrimaryGenreName(String primaryGenreName) {
		this.primaryGenreName = primaryGenreName;
	}

	public Integer getPrimaryGenreId() {
		return primaryGenreId;
	}

	public void setPrimaryGenreId(Integer primaryGenreId) {
		this.primaryGenreId = primaryGenreId;
	}
}
```

### Album (Album.java)
```
package com.coresoftware.MusicLib.model;

public class Album extends ITunesEntity {
	// Album
	private Integer artistId;
	private Integer amgArtistId;
	private String artistName;
	private String primaryGenreName;
	private String collectionType;
	private Integer collectionId;
	private String collectionName;
	private String collectionCensoredName;
	private String artistViewUrl;
	private String collectionViewUrl;
	private String artworkUrl60;
	private String artworkUrl100;
	private String collectionPrice;
	private String collectionExplicitness;
	private Integer trackCount;
	private String copyright;
	private String country;
	private String currency;
	private String releaseDate;

	public final String wrapperType = "collection";



	public Integer getArtistId() {
		return artistId;
	}

	public void setArtistId(Integer artistId) {
		this.artistId = artistId;
	}

	public Integer getAmgArtistId() {
		return amgArtistId;
	}

	public void setAmgArtistId(Integer amgArtistId) {
		this.amgArtistId = amgArtistId;
	}

	public String getArtistName() {
		return artistName;
	}

	public void setArtistName(String artistName) {
		this.artistName = artistName;
	}

	public String getPrimaryGenreName() {
		return primaryGenreName;
	}

	public void setPrimaryGenreName(String primaryGenreName) {
		this.primaryGenreName = primaryGenreName;
	}

	public String getCollectionType() {
		return collectionType;
	}

	public void setCollectionType(String collectionType) {
		this.collectionType = collectionType;
	}

	public Integer getCollectionId() {
		return collectionId;
	}

	public void setCollectionId(Integer collectionId) {
		this.collectionId = collectionId;
	}

	public String getCollectionName() {
		return collectionName;
	}

	public void setCollectionName(String collectionName) {
		this.collectionName = collectionName;
	}

	public String getCollectionCensoredName() {
		return collectionCensoredName;
	}

	public void setCollectionCensoredName(String collectionCensoredName) {
		this.collectionCensoredName = collectionCensoredName;
	}

	public String getArtistViewUrl() {
		return artistViewUrl;
	}

	public void setArtistViewUrl(String artistViewUrl) {
		this.artistViewUrl = artistViewUrl;
	}

	public String getCollectionViewUrl() {
		return collectionViewUrl;
	}

	public void setCollectionViewUrl(String collectionViewUrl) {
		this.collectionViewUrl = collectionViewUrl;
	}

	public String getArtworkUrl60() {
		return artworkUrl60;
	}

	public void setArtworkUrl60(String artworkUrl60) {
		this.artworkUrl60 = artworkUrl60;
	}

	public String getArtworkUrl100() {
		return artworkUrl100;
	}

	public void setArtworkUrl100(String artworkUrl100) {
		this.artworkUrl100 = artworkUrl100;
	}

	public String getCollectionPrice() {
		return collectionPrice;
	}

	public void setCollectionPrice(String collectionPrice) {
		this.collectionPrice = collectionPrice;
	}

	public String getCollectionExplicitness() {
		return collectionExplicitness;
	}

	public void setCollectionExplicitness(String collectionExplicitness) {
		this.collectionExplicitness = collectionExplicitness;
	}

	public Integer getTrackCount() {
		return trackCount;
	}

	public void setTrackCount(Integer trackCount) {
		this.trackCount = trackCount;
	}

	public String getCopyright() {
		return copyright;
	}

	public void setCopyright(String copyright) {
		this.copyright = copyright;
	}

	public String getCountry() {
		return country;
	}

	public void setCountry(String country) {
		this.country = country;
	}

	public String getCurrency() {
		return currency;
	}

	public void setCurrency(String currency) {
		this.currency = currency;
	}

	public String getReleaseDate() {
		return releaseDate;
	}

	public void setReleaseDate(String releaseDate) {
		this.releaseDate = releaseDate;
	}
}
```

### ITunesEntity (ITunesEntity.java)
```
package com.coresoftware.MusicLib.model;

import com.fasterxml.jackson.annotation.JsonSubTypes;
import com.fasterxml.jackson.annotation.JsonTypeInfo;

@JsonTypeInfo(
		use = JsonTypeInfo.Id.NAME, // Use the name of the type as the discriminator
		include = JsonTypeInfo.As.PROPERTY, // The type info is a property in JSON
		property = "wrapperType" // The JSON property name that determines the type
)
@JsonSubTypes({
		@JsonSubTypes.Type(value = Artist.class, name = "artist"),
		@JsonSubTypes.Type(value = Album.class, name = "collection")
})

public abstract class ITunesEntity {

}
```

### ITunesResult (ITunesResult.java)
```
package com.coresoftware.MusicLib.model;

import java.util.List;

public class ITunesResult {

	private Integer resultCount;
	private List<ITunesEntity> results;

	public Integer getResultCount() {
		return resultCount;
	}

	public void setResultCount(Integer resultCount) {
		this.resultCount = resultCount;
	}

	public List<ITunesEntity> getResults() {
		return results;
	}

	public void setResults(List<ITunesEntity> results) {
		this.results = results;
	}
}
```

## Rest Controller
### ITunes Controller (ITunesController.java)
```
package com.coresoftware.MusicLib.rest;

import com.coresoftware.MusicLib.service.ITunesService;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class ITunesController {

	// getAlbumByName(Artist id, AlbumName name);
	// getAlbumById(Artist id, AlbumId, aid);

	// getAlbums(Artist id);


	private final ITunesService albumService;

	public ITunesController(ITunesService albumService) {
		this.albumService = albumService;
	}

	@GetMapping("/album")
	@ResponseBody
	public Object getAllAlbumsOld() {
		System.out.println("getAllAlbumsOld: ");
		return albumService.getAllAlbumByArtistId(12);
	}

	/* Methode .........: getAllAlbums()
	 * Description .....: Get all Albums from ITunes RestAPI by ArtistId
	 * Arguments #1 ....: Integer artist_id
	 * Example .........: http://localhost:8080/api/getAllAlbum?artist_id=78500
	 * Return Value ....: Artist[]
	 */
	@GetMapping("/getAllAlbum")
	@ResponseBody
	public Object getAllAlbums(Integer artist_id) {

		System.out.println("XXX getAllAlbums: " + artist_id.intValue());
		return albumService.getAllAlbumByArtistId(artist_id);
	}
}
```

## Service
### ITunes Service (ITunesService.haml)
```
package com.coresoftware.MusicLib.service;

import com.coresoftware.MusicLib.model.ITunesResult;
import com.coresoftware.MusicLib.model.ITunesEntity;
import org.springframework.boot.web.client.RestTemplateBuilder;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.http.converter.HttpMessageConverter;
import org.springframework.http.converter.json.MappingJackson2HttpMessageConverter;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

import java.util.*;

@Service
public class ITunesService {
	private final RestTemplate restTemplate;
	final String ROOT_URI = "https://itunes.apple.com";

	public ITunesService(RestTemplateBuilder restTemplateBuilder) {
		this.restTemplate = restTemplateBuilder.build();
		List<HttpMessageConverter<?>> messageConverters = new ArrayList<>();
		MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
		converter.setSupportedMediaTypes(Collections.singletonList(MediaType.ALL));
		messageConverters.add(converter);
		this.restTemplate.setMessageConverters(messageConverters);
	}

	/*
	 * Methode .........: getAllAlbumByArtistId()
	 * Description .....: Get all Albums from ITunes RestAPI by ArtistId
	 * Arguments #1 ....: Integer artist_id
	 * Example .........: http://localhost:8080/api/getAllAlbum?artist_id=78500
	 *
	 * @param  artist_id  an absolute URL giving the base location of the image
	 * @return            ArrayList of Album's by a given Artist
	 */
	public List<ITunesEntity> getAllAlbumByArtistId(Integer artist_id) {
		String search_str = String.format("%s/lookup?id=%d&entity=album", ROOT_URI, artist_id);
		List<ITunesResult> entity = new ArrayList<>();

		ResponseEntity<ITunesResult> response = restTemplate.getForEntity(search_str, ITunesResult.class);

		return response.getBody().getResults();
	}
}
```

## Templates
### Artist Confirmation (artist-confirmation.haml)
```
```

### Artist Form (artist-form.haml)

```
```
