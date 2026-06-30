module.exports = function (eleventyConfig) {
  eleventyConfig.addPassthroughCopy("admin");
  eleventyConfig.addPassthroughCopy("imagenes");

  const meses = ["enero","febrero","marzo","abril","mayo","junio","julio","agosto","septiembre","octubre","noviembre","diciembre"];
  eleventyConfig.addFilter("readableDate", function (dateObj) {
    if (!dateObj) return "";
    const d = new Date(dateObj);
    return `${d.getUTCDate()} de ${meses[d.getUTCMonth()]} de ${d.getUTCFullYear()}`;
  });

  eleventyConfig.addCollection("avisos", function (collectionApi) {
    return collectionApi.getFilteredByGlob("content/avisos/*.md").sort((a, b) => b.date - a.date);
  });

  eleventyConfig.addCollection("noticias", function (collectionApi) {
    return collectionApi.getFilteredByGlob("content/noticias/*.md").sort((a, b) => b.date - a.date);
  });

  eleventyConfig.addCollection("videos", function (collectionApi) {
    return collectionApi.getFilteredByGlob("content/videos/*.md").sort((a, b) => b.date - a.date);
  });

  return {
    dir: {
      input: ".",
      output: "_site",
      includes: "_includes",
    },
  };
};
